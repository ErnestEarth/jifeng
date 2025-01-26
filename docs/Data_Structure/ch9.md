# ch9 高级搜索树

## 1. 伸展树

【局部性】

- 时间局部性：刚被访问过的数据，极有可能很快地再次被访问。
- 空间局部性：下一将要访问的节点，极有可能就在刚被访问过节点的附近。
- 自适应链表：节点一旦被访问，随机移动到最前端。在 BST 中，节点一旦被访问，随机调整到树根。

【逐层伸展】节点 $v$ 一旦被访问，随机被推送至根，或者说 “爬”，一步一步地往上爬，自下而上，逐层旋转。最坏情况下，旋转次数呈周期性的算术级数，每一周期累计 $\Omega(n^2)$，分摊 $\Omega(n)$。

【双层伸展】每次向上追溯两层，反复考察祖孙三代，$g = parent(p), p = parent(v), v$，根据它们的相对位置，经两次旋转，使 $v$ 上升两层，成为子树根。节点访问之后，对应路径的长度随机折半，最坏情况不致持续发生，伸展操作分摊仅需 $\cal{O}(\log n)$ 时间。

```cpp
// 伸展算法
template <typename T> BinNodePosi<T> Splay<T>::splay(BinNodePosi<T> v) {
    BinNodePosi<T> p, g;	// 父亲，祖父
    while ((p = v->parent) && (g = p->parent)) {	// 自下而上，反复双层伸展
        BinNodePosi<T> gg = g->parent;	// 曾祖父
        switch ((IsLChild(p) << 1) | IsLChild(v)) {
            case 0b00 :  	// zig-zig
                g->attachLc(p->rc); p->attachLc(v-rc);
                p->attachRc(g); v->attachRc(p); break;
            case 0b01 :  	// zig-zag
                p->attachRc(v->lc); g->attachLc(v-rc);
                v->attachRc(g); v->attachLc(p); break;
            case 0b10 :  	// zag-zig
                p->attachLc(v->rc); g->attachRc(v-lc);
                v->attachLc(g); v->attachRc(p); break;
            default :    	// zag-zag
                g->attachRc(p->lc); p->attachRc(v-lc);
                p->attachLc(g); v->attachLc(p); break;
        }
        
        // 向上连接，更新高度
        if (!gg) v->parent = NULL;
        else (g == gg->lc) ? gg->attachLc(v) : gg->attachRc(v);
        g->updateHeight(); p->updateHeight(); v->updateHeight();
    }
    
    // 若 p 果真是根，只需再额外单层伸展一次
    if (p = v->parent) {
        if (IsLChild(v)) {
            p->attachLc(v-rc);
            v->attachRc(p);
        }
        else {
            p->attachRc(v->lc);
            v->attachLc(p);
        }
        p->updateHeight();
        v->updateHeight();
    }
    
    // 伸展完成，v 抵达树根
    v->parent = NULL;
    return v;
}
```

```cpp
// 查找算法
template <typename T> 
BinNodePosi<T> & Splay<T>::search(const T & e) {
    BinNodePosi<T> p = BST<T>::search(e);
    _root = p ? splay(p) : _hot ? splay(_hot) : NULL;
    return _root;
}

// 插入算法
template <typename T>
BinNodePosi<T> Splay<T>::insert(const T & e) {
    if (!_root) {
        _size = 1;
        return _root = new BinNode<T>(e);
    }
    
    BinNodePosi<T> t = search(e);
    if (e == t->data) return t;
    
    if (t->data < e) {
        _root = t->parent = new BinNode<T>(e, NULL, t, t->rc);
        t->rc = NULL;
    }
    else {
        t->parent = _root = new BinNode<T>(e, NULL, t->lc, t);
        t->lc = NULL;
    }
    
    _size++;
    t->updateHeightAbove();
    return _root;
}

// 删除算法
template <typename T>
bool Splay<T>::remove(const T & e) {
    if (!_root || (e != search(e)->data)) return false;
    BinNodePosi<T> L = _root->lc, R = _root->rc;
    delete _root;
    
    if (!R) {
        if (L) L->parent = NULL;
        _root = L;
    }
    else {
        _root = R;
        R->parent = NULL;
        search(e);
        _root->attachLc(L);
    }
    
    _size--;
    if (_root) _root->updateHeight();
    return true;
}
```

【综合评价】

- 无需记录高度或平衡因子；编程实现简单，优于 AVL 树；分摊复杂度 $\cal{O}(\log n)$，与 AVL 树相当。

- 局部性强，缓存命中率极高时，效率甚至可以更高（自适应的 $\cal{O}(\log k)$），任何连续的 $m$ 次查找，仅需 $\cal{O}(m\log k + n\log n)$ 时间。
- 若反复地顺序访问任一子集，分摊成本仅为常数。
- 不能杜绝单次最坏情况，不适用于对效率敏感的场合。

## 2. B- 树

【现实背景】

- 存储器容量的增长速度远小于应用问题规模的增长速度。
- 在特定工艺及成本下，存储器都是容量与速度的折中产物。
- 实用的存储系统，由不同类型的存储器级联而成，以综合其各自的优势。
- 在外存读写 $\tt 1\ B$，与读写 $\tt 1\ KB$ 几乎一样快。以页为单位，借助缓冲区批量访问，可大大缩短单位字节的平均访问时间。

【分级存储】利用数据访问的局部性

- 机制与策略：常用的数据，复制到更高层、更小的存储器中，找不到，才向更低层、更大的存储器索取。
- 算法的实际运行时间，主要取决于相邻存储级别之间数据传输（$\tt I/O$）的速度与次数。

【平衡的多路搜索树】每 $d$ 代合并为超级节点，$m=2^d$ 路，$m-1$ 个关键码，逻辑上与 BBST 完全等价。多级存储系统中使用 B- 树，可针对外部查找，大大减少 $\tt I/O$ 次数。B- 树充分利用外存的批量访问，将此特点转化为优点，每下降一层，都以超级节点为单位，读入一组关键码。

【$m$ 阶 B- 树】即 $m$ 路完全平衡搜索树（$m\ge 3$），

- 外部节点的深度统一相等，约定以此深度作为树高 $h$；
- 叶节点的深度统一相等，为 $h-1$；
- 内部节点各含 $n\le m-1$ 个关键码：$K_1<K_2<K_3<...<K_n$，各有 $n+1\le m$ 个分支：$A_0,A_1,A_2, ..., A_n$。
- 反过来，分支数也不能太少，树根：$2\le n+1$，其余：$\lceil m/2\rceil \le n+1$，因此也称作 $(\lceil m/2\rceil,m)-$ 树。

## 3. 红黑树

【并发性】修改之前先加锁，完成后解锁，访问延迟主要取决于 $lock\sim unlock$ 周期。对于 BST 而言，每次修改过程中，唯结构有变处才需加锁，访问延迟主要取决于这类局部之数量。$\tt Splay$ 结构变化剧烈，最差可达 $\cal{O}(n)$，$\tt AVL$ 在 `remove()` 时为 $\cal{O}(\log n)$，红黑树无论 `insert` 还是 `remove`，均不超过 $\cal{O}(1)$。

【持久性】支持对历史版本的访问。

【压缩存储】大量共享，少量更新，每个版本的新增复杂度，仅为 $\cal{O}(\log n)$。

【红黑树】由红、黑两类节点组成的 BST，统一引入外部节点 NULL，成为真二叉树。

- 树根：必为黑色
- 外部节点：均为黑色
- 红节点：只能有黑孩子及黑父亲
- 外部节点：黑深度（黑的真祖先数目）相等，即根（全树）的黑高度，子树的黑高度（即后代 NULL 的相对黑深度）
- 将红节点提升至与其（黑）父亲等高，于是每棵红黑树，都对应于一棵 $(2,4)-$ 树。
- 包含 $n$ 个内部节点的红黑树 $T$，高度 $h = \cal{O}(\log n)$，$\log_2(n+1)\le h\le 2\log_2(n+1)$。
- 若 $T$ 高度为 $h$，红 / 黑高度为 $R/H$，则 $H\le h \le R+H \le 2H$。
- 若 $T$ 所对应的 $B-$ 树为 $T_B$，则 $H$ 即是 $T_B$ 的高度。$T_B$ 的每个节点，都恰好包含 $T$ 的一个黑节点，于是 $H\le \log_{\lceil4/2\rceil} \frac{n+1}{2} + 1 =\log_2(n+1)$。