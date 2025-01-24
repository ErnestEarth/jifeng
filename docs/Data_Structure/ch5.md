# ch5 二叉树

## 1. 树

【应用】层次结构的表示：表达式、文件系统、URL

【数据结构】综合性，兼具向量和链表的优点，兼顾高效的查找、插入、删除

【半线性】不再是简单的线性结构，但在确定某种次序之后，具有线性特征。

【树】树是极小连通图、极大无环图 $T=(V;E)$，指定任一节点 $r\in V$ 作为根后，称为有根树。若 $T_1,T_2,..,T_d$ 为有根树，那么 $T = ((\cup_iV_i)\cup\{r\},(\cup_iE_i)\cup\{<r,r_i>|1\le i\le d\})$ 也是有根树。

【子树与度】相对于 $T$，$T_i$ 称作以 $r_i$ 为根的子树，记作 $T_i = subtree(r_i)$。$r_i$ 称作 $r$ 的孩子，$r_i$ 之间互称兄弟，$r$ 为其父亲，$d = degree(r)$ 为 $r$ 的（出）度。可证明 $e = |E| = \sum_{v\in V}degree(v) = n-1 = \Theta(n)$。

【有序树】若指定 $T_i$ 作为 $T$ 的第 $i$ 棵子树，$r_i$ 作为 $r$ 的第 $i$ 个孩子，则 $T$ 称作有序树。

【路径与环】$V$ 中的 $k+1$ 个节点，通过 $V$ 中的 $k$ 条边依次相连，构成一条路径 / 通路，$\pi = \{(v_0,v_1),(v_1,v_2),(v_2,v_3),..,(v_{k-1},v_k)\}$，路径长度即所含边数 $|\pi| = k$。如果满足 $v_k=v_0$，则称为回路 / 环，如果覆盖所有节点各一次，称作周游。

【无环连通图】节点之间均有路径称作连通图，如果所有路径中不存在环，称作无环图。树是一个无环连通图。因此任一节点 $v$ 与根节点之间存在唯一路径，于是以 $|path(v)|$ 为指标，可对所有节点做等价类划分。不致歧义时，路径、节点和子树可以相互指代：$path(v) \sim v\sim subtree(v)$。

【节点深度】$depth(v) = |path(v)|$，$path(v)$ 上的节点，均为 $v$ 的祖先，$v$ 是它们的后代。其中除自身外，是真祖先 / 后代。半线性的特征，使得在任一深度，$v$ 的祖先（后代）若存在，则必然（未必）唯一。根节点是所有节点的公共祖先，深度为 $0$。

【节点高度】没有后代的节点称作叶子，所有叶子深度中的最大者，称作（子）树（根）的高度，$height(v) = height(subtree(v))$。特别地，空树的高度取作 $-1$。$depth(v)+height(v)\le height(T)$。

## 2. 树的表示

【父亲表示法】除根节点外，任一节点有且仅有一个父节点。可以把节点组织为一个序列，各自记录 $data$ 和 $parent$。

【孩子表示法】同一节点的所有孩子，各成一个序列，各序列的长度，即对应节点的度数。

【父亲孩子表示法】两种表示法的优势进行互补。

## 3. 二叉树

【二叉树】节点度数不超过 $2$，孩子（子树）可以区分左右（隐含有序）。

【孩子兄弟表示法】可以将有根且有序的多叉树转化并表示为二叉树。

【基数】设度数为 $0,1,2$ 的节点各有 $n_0,n_1,n_2$ 个

- 边数 $e = n-1 = n_1 +2n_2$。
- 叶结点数 $n_0 = n_2+1$。
- 结点数 $n =n_0 + n_1 + n_2 = 1 + n_1 + 2n_2$。
- 当 $n_1 = 0$ 时，有 $e = 2n_2$，$n_0 = n_2 + 1 =(n+1)/ 2$。
- 深度为 $k$ 的节点，至多 $2^k$ 个。
- $n$ 个节点，高 $h$ 的二叉树满足 $h+1\le n\le 2^{h+1}- 1$。

- 当 $n=h+1$ 时，退化为一条单链。
- 当 $n=2^{h+1}- 1$ 时，即所谓满二叉树。

【真二叉树】通过引入 $n_1+2n_0$ 个外部节点，可使原有节点度数统一为 $2$。如此，可将任一二叉树转化为真二叉树。转换之后全树自身的复杂度并未实质增加，对于红黑树之类的结构，真二叉树可以简化描述、理解、实现和分析。

【完全二叉树】叶节点仅限于最低两层，底层叶子，均居于次底层叶子左侧（相对于 LCA），除末节点的父亲，内部节点均有双子。叶节点不少于内部节点，但至多多出一个。

## 4. 二叉树遍历

【遍历】按照某种次序访问树中各节点，每个节点被访问恰好一次。

【藤】起始于根的左侧通路，即长子通路。

【先序遍历】沿着藤，整个遍历过程可分解为两个阶段：自上而下访问藤上节点；自下而上遍历各右子树。各右子树的遍历彼此独立，自成一个任务。

```cpp
template <typename T, typename VST> 
static void visitAlongVine(BinNodePosi<T> x, VST & visit, Stack<BinNodePosi<T> > & S) {
    while (x) {						// 反复地
        visit(x->data);				// 访问当前节点
        S.push(x->rc);				// 右子树入栈
        x = x->lc;					// 沿藤下行
    }
}
// 先序遍历迭代实现：#push = #pop = #visit = O(n) = 均摊 O(1)
template <typename T, typename VST>
void travPre_I2(BinNodePosi<T> x, VST & visit) {
    Stack<BinNodePosi<T> > S;		// 辅助栈
    while (true) {					// 以右子树为单位，逐批访问节点
        visitAlongVine(x, visit, S);// 访问子树 x 的藤，各右子树的根入栈缓冲
        if (S.empty()) break;		// 栈空即退出
        x = S.pop();				// 弹出下一个右子树的根
    }
}
```

【中序遍历】沿着藤，遍历过程可自底向上分解为 $d+1$ 步迭代：访问藤上节点，再遍历其右子树。各右子树的遍历彼此独立，自成一个任务。

```cpp
template <typename T>
static void goAlongVine(BinNodePosi<T> x, Stack<BinNodePosi<T> > & S) {
    while (x) {
        S.push(x);
        x = x->lc;
    } // 逐层深入，沿藤蔓各节点依次入栈 
}
// 中序遍历迭代实现
template <typename T, typename VST>
void travIn_I1(BinNodePosi<T> x, VST & visit) {
    Stack<BinNodePosi<T> > S;		// 辅助栈
    while (true) {					// 反复地
        goAlongVine(x, S);			// 从当前节点出发，逐批入栈
        if (S.empty()) break;		// 栈空即退出
        x = S.pop();				// x 的左子树或为空，或已遍历
        visit(x->data);				// 立即访问之
        x = x->rc;					// 转向右子树
    }
}
```

【后序遍历】沿藤分解，从根出发下行，尽可能沿左分支，实不得已，才沿右分支。最后一个节点，必是叶子，而且是按中序次序最靠左者，也是递归版中 `visit()` 首次执行处，这片叶子，将首先接受访问。

```cpp
template <typename T>
static void gotoLeftmostLeaf(Stack <BinNodePosi<T> > & S) {
    while (BinNodePosi<T> x = S.top()) {	// 自顶向下反复检查栈顶节点
        if (HasLChild(x)) {					// 尽可能向左，在此之前
            if (HasRChild(X))				// 若有右孩子，则
                S.push(x->rc);				// 优先入栈
            S.push(x->lc);					// 然后转向左孩子
        } else {							// 实不得已
            S.push(x->rc);					// 才转向右孩子
        }
    }
    S.pop();								// 弹出栈顶的空节点
}
// 后序遍历迭代实现
template <typename T, typename V>
void travPost_I(BinNodePosi<T> x, V & visit) {
    Stack<BinNodePosi<T> > S;				// 辅助栈
    if (x) S.push(x);						// 根节点首先入栈
    while (!S.empty()) {					// x 始终为当前节点
        if (S.top() != x->parent)			// 若栈顶非 x 之父
            gotoLeftmostLeaf(S);			// 则转入右兄子树
        x = S.pop();						// 弹出栈顶（即前一节点之后继）
        visit(x->data);						// 并随即访问之
    }
}
```

## 5. 重构

- 通过先序 / 后序与中序序列可以重构二叉树。

- 通过先序与后序可以重构真二叉树。

【增强序列】假想地认为，每个 NULL 也是 “真实” 节点，并在遍历时一并输出。每次递归返回，同时输出一个事先约定的元字符 `^`。若将遍历序列表示为一个 `Iterator`，则可将其定义为 `Vector<BinNode<T> *>`。于是在增强的遍历序列中，这类 “节点” 可统一记作 NULL。

可归纳证明：在增强的先序 / 后序遍历序列中，任一子树依然对应于一个子序列，而且其中的 NULL 节点恰比非 NULL 节点多一个。如此，通过对增强序列分而治之，即可重构原树。

