# ch8 二叉搜索树

## 1. 二叉搜索树

【顺序性】任一节点均不小 / 大于其左 / 右后代。

【单调性】BST 的中序遍历，必然单调非降。

【查找】从根节点出发，逐步地缩小查找范围，直到发现目标（命中），或抵达空树（未命中）。对照中序遍历序列可见，整个过程可视作是在仿效有序向量的二分查找。

```cpp
template <typename T> 
BinNodePosi<T> & BST<T>::search(const T & e) {
    if (!_root || e == _root->data) {
        _hot = NULL;
        return _root;
    }
    
    for (_hot = _root; ; ) {
        BinNodePosi<T> & v = (e < _hot->data) ? _hot->lc : _hot->rc;
        if (!v || e == v->data) return v;
        _hot = v;
    }
}
```

【插入】先借助 `search(e)`，确定插入位置与方向。若 $e$ 尚不存在，则再将新节点作为叶子插入：`_hot` 为新节点的父亲，`v = search(e)` 为 `_hot` 对新孩子的引用。于是，只需令 `_hot` 通过 $v$ 指向新节点。

```cpp
template <typename T>
BinNodePosi<T> BST<T>::insert(const T & e) {
    BinNodePosi<T> & x = search(e);
    if (x) return x;
    
    x = new BinNode<T>(e, _hot);
    _size++;
    x->updataHeightAbove();
    return x;
}
```

【删除】若 $x$ 的某一子树为空，则可将其替换为另一子树。若 $x$ 左、右孩子并存，则找到 $x$ 的后继 `w = x.succ()`，交换 $x$ 与 $w$（必无左孩子），于是问题转化为删除 $w$，可按前一情况处理。

```cpp
template <typename T>
static BinNodePosi<T> removeAt(BinNodePosi<T> & x, BinNodePosi<T> & hot) {
    BinNodePosi<T> w = x;
    BinNodePosi<T> succ = NULL;
    
    if (!HasLChild(x)) succ = x = x->rc;
    else if (!HasRChild(X)) succ = x = x->lc;
    else {
        w = w->succ();
        swap(x->data, w->data);
        BinNodePosi<T> u = w->parent;
        (u == x ? u->rc : u->lc) = succ = w->rc;
    }
    
    hot = w->parent;
    if (succ) succ->parent = hot;
    delete w;
    return succ;
}

template <typename T>
bool BST<T>::remove(const T & e) {
    BinNodePosi<T> & x = search(e);
    if (!x) return false;
    
    removeAt(x, _hot);
    _size++;
    _hot->updateHeightAbove();
    return true;
}
```

## 2. 平衡树

BST 主要接口 `search()`、`insert()` 和 `remove()` 的运行时间在最坏情况下，均线性正比于其高度 $\cal{O}(h)$。若不能有效地控制树高，就无法体现出 BST 相对于向量、列表等数据结构的明显优势。比如在最（较）坏情况下，二叉搜索树可能彻底地（接近地）退化为列表，此时的性能不仅没有提高，而且因为结构更为复杂，反而会在常数意义上下降。

【理想平衡】节点数目固定时，兄弟子树的高度越接近平衡，全树也将倾向于更低。由 $n$ 个节点组成的二叉树，高度不致低于 $\lfloor \log_2 n\rfloor$，达到这一下界时，称作理想平衡。大致相当于完全树甚至满树。

【渐近平衡】理想平衡出现的概率极低、维护的成本过高，故须适当地放松标准：高度渐近地不超过 $\cal{O}(\log n)$ 即可接受。渐近平衡的 BST，称作平衡二叉搜索树（BBST）。

【等价 BST】

- 上下可变：连接关系不尽相同，承袭关系可能颠倒
- 左右不乱：中序遍历序列完全一致，全局单调非降

【限制条件】各种 BBST 都可视作 BST 的某一子集，相应地满足精心设计的限制条件

- 单次动态修改操作后，至多 $\cal{O}(\log n)$ 处局部不再满足限制条件（可能相继违反，未必同时）
- 可在 $\cal{O}(\log n)$ 时间内，使这些局部（以至全树）重新满足

【AVL 树的平衡因子】$balFac(v) = height(lc(v)) - height(rc(v))$，$\forall v\in AVL$，$|balFac(v)|\le 1$。AVL 树未必理想平衡，但必然渐近平衡。

【AVL 树】高度为 $h$ 的 AVL 树，至少包含 $S(h) = fib(h+3) - 1$ 个节点。反过来，由 $n$ 个节点构成的 AVL 树，高度不超过 $\cal{O}(\log n)$。

【Fibonaccian 树】高度为 $h$，规模恰为 $S(h) = fib(h+3) - 1$ 的 AVL 树。是最瘦的、临界的 AVL 树。

【插入操作】

![单旋](img/%E5%B9%B3%E8%A1%A1%E6%A0%91%E6%8F%92%E5%85%A5%E5%8D%95%E6%97%8B.png)

![双旋](img/%E5%B9%B3%E8%A1%A1%E6%A0%91%E6%8F%92%E5%85%A5%E5%8F%8C%E6%97%8B.png)

```cpp
template <typename T>
BinNodePosi<T> AVL<T>::insert(const T & e) {
    BinNodePosi<T> & x = search(e);
    if (x) return x;
    
    BinNodePosi<T> xx = x = new BinNode<T>(e, _hot);
    _size++;
    
    for (BinNodePosi<T> g = _hot; g; g->updateHeight(), g = g->parent) {
        if (!AvlBalanced(g)) {
            rotateAt(tallerChild(tallerChild(g)));
            break;
        }
    }
    
    return xx;
}
```

【删除操作】

![单旋](img/%E5%B9%B3%E8%A1%A1%E6%A0%91%E5%88%A0%E9%99%A4%E5%8D%95%E6%97%8B.png)

![双旋](img/%E5%B9%B3%E8%A1%A1%E6%A0%91%E5%88%A0%E9%99%A4%E5%8F%8C%E6%97%8B.png)

```cpp
template <typename T>
bool AVL<T>::remove(const T & e) {
    BinNodePosi<T> & x = search(e);
    if (!x) return false;
    
    removeAt(x, _hot);
    _size--;
    
    for (BinNodePosi<T> g = _hot; g; g->updateHeight(), g = g->parent) {
        if (!AvlBalanced(g)) {
            rotateAt(tallerChild(tallerChild(g)));
        }
    }
    
    return true;
}
```

【$3+4$ 平衡重构】设 $g$ 为最低的失衡节点，沿最长分支考察祖孙三代 $g\sim p\sim v$，按中序遍历次序，重命名为 $a<b<c$。它们总共拥有四棵子树（或为空），按中序遍历次序，重命名为 $T_0<T_1<T_2<T_3$。将原先以 $g$ 为根的子树，替换为以 $b$ 为根的新子树，等价变换，保持中序遍历次序：$T_0<a<T_1<b<T_2<c<T_3$。

```cpp
template <typename T> BinNodePosi<T> BST<T>::connect34(
	BinNodePosi<T> a, BinNodePosi<T> b, BinNodePosi<T> c,
    BinNodePosi<T> T0, BinNodePosi<T> T1, BinNodePosi<T> T2, BinNodePosi<T> T3) {
    a->lc = T0; if (T0) T0->parent = a;
    a->rc = T1; if (T1) T1->parent = a;
    c->lc = T2; if (T2) T2->parent = c;
    c->rc = T3; if (T3) T3->parent = c;
    b->lc = a; a->parent = b;
    b->rc = c; c->parent = b;
    a->updateHeight(); c->updateHeight(); b->updateHeight();
    return b;
}

template <typename T>
BinNodePosi<T> BST<T>::rotateAt(BinNodePosi<T> v) {
    BinNodePosi<T> p = v->parent;
    int TurnV = IsRChild(v);
    BinNodePosi<T> g = p->parent;
    int TurnP = IsRChild(p);
    
    BinNodePosi<T> r = (TurnP == TurnV) ? p : v;
    (FromParentTo(g) = r)->parent = g->parent;
    switch((TurnP << 1) | TurnV) {
        case 0b00: return connect34(v, p, g, v->lc, v->rc, p->rc, g->rc);
        case 0b01: return connect34(p, v, g, p->lc, v->lc, v->rc, g->rc);
        case 0b10: return connect34(g, v, p, g->lc, v->lc, v->rc, p->rc);
        default:   return connect34(g, p, v, g->lc, p->lc, v->lc, v->rc);
    }
}
```

【综合评价】

- 优点：无论查找、插入或删除，最坏情况下的复杂度均为 $\cal{O}(\log n)$，$\cal{O}(n)$ 的存储空间。
- 缺点：借助高度或平衡因子，为此需改造元素结构，或额外封装，实测复杂度与理论值尚有差距。
    - 插入 / 删除后的旋转，成本不菲
    - 删除操作后，最多需旋转 $\Omega(\log n)$ 次（Knuth：平均仅 $0.21$ 次）
    - 若需频繁进行插入 / 删除操作，未免得不偿失，单次动态调整后，全树拓扑结构的变化量可能高达 $\Omega(\log n)$