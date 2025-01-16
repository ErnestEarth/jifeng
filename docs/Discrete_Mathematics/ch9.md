# ch9 实数集合与集合的基数

## 1. 实数集合

【整数】对自然数集合 $N$，令 $Z_+ = N - \{0\}$，$Z_- = \{<0,n> | n \in Z_+\}$，$Z = Z_+\cup \{0\}\cup Z_-$。

【相反数】一个整数的相反数分别是

- $-n = <0,n>$，当 $n\in Z_+$
- $-0=0$
- $-<0,n> = n$，当 $n\in Z_+$
- 在集合 $Z$ 上定义小于等于关系 $\le_Z$ 为，对任意的 $x,y\in Z$，$x \le_Z y$ 当且仅当 $(x\in N\land y\in N\land x\le_N y) \lor (x\in Z \land y\in N)\lor (x\in Z_- \land y\in Z_-\land -y\le_N -x)$。
- 在集合 $Z$ 上定义小于关系 $<_Z$ 为，对任意的 $x,y\in Z, x<_Z y$ 当且仅当 $(x\le_Z y)\land(x\ne y)$。

【等价关系 $\cong$】对整数集合 $Z$，令 $Q_1 = Z\times (Z-\{0\}) = \{<a,b> | a\in Z\land b\in Z\land b\ne 0\}$，并称 $Q_1$ 是 $Z$ 上的因式的集合。对 $<a,b>\in Q_1$，可以用 $a/b$ 代替 $<a,b>$。在 $Q_1$ 上定义关系 $\cong$ 为对任意的 $a/b\in Q_1$，$c/d\in Q_1$，$a/b \cong c/d$ 当且仅当 $a\cdot d = b\cdot c$，其中 $a\cdot d$ 是在 $Z$ 上定义的乘法，$=$ 是 $Z$ 上的相等关系。

【有理数集合】$Q = Q_1/\cong$，即 $Q$ 是集合 $Q_1$ 对等价关系 $\cong$ 的商集，则称 $Q$ 的元素为有理数，一般用 $a/b$ 表示 $Q$ 中的元素 $[<a,b>_{\cong}]$，并习惯上取 $a,b$ 是互素的整数，且 $b>0$。

- 在 $Q$ 上定义小于等于关系 $\le_Q$ 为，对任意的 $a/b,c/d\in Q$，$a/b\le_Q c/d$ 当且仅当 $a\cdot d\le_Z b\cdot c$。

【实无穷】把无限的整体本身作为一个现成的单位，是已经构造完成了的东西，换言之，即是把无限对象看成可以自我完成的过程或无穷整体。

【基本函数】如果 $f:N\to Q$ 满足有界，且单调非递减，则称 $f$ 是一个基本函数，或有界非递减函数。函数值 $f(0),f(1),f(2),..,f(n),..$ 称为一个基本序列，它有时写为 $r_0,r_1,r_2,..,r_n,..$

【定理】当 $f:N\to Q$ 取常数值时，$f$ 是基本函数。即对任意的 $r\in Q$，$r,r,r..$ 是一个基本序列。

【定理】存在不是常值函数的基本函数。$f(n) = 1 - 1/(n+1)$。

对基本函数的集合 $B$，定义 $B$ 上的关系为 $\cong$，对任意的 $f,g\in B$，$f\cong g$ 当且仅当 $(\forall \epsilon)((\epsilon \in Q \land \epsilon > 0) \to (\exists n)(n\in N \land (\forall m)((m\in N\land n\le m)\to |f(m)-g(m)| < \epsilon)))$。置换上说，$f\cong g$ 等价于 $f$ 和 $g$ 的序列的极限相同。$f(n) = 1 - 1/(n+1)$ 和 $g(n) = 1$，有 $f\cong g$。

【定理】设 $f:N\to Q$，$g: N\to Q$ 且都是常值函数，且 $f\cong g$，则 $f=g$。

【实数集】令 $R = B/\cong$，即 $R$ 是基本函数的集合 $B$ 对等价关系 $\cong$ 的商集，则称 $R$ 的元素为实数，称 $R$ 为实数集合。$X$ 的等价类中有一个常数函数 $f(n) = r$，则 $x$ 为一个有理数，否则 $x$ 是无理数。

- 在基本函数的集合 $B$ 上定义小于关系 $<_B$ 为，对任意的 $f,g\in B$，$f<_B g$ 当且仅当 $(\exists \epsilon)((\epsilon \in Q\land 0 < \epsilon)\land (\exists n)(n\in N\land(\forall m)((m\in N\land n\le m)\to g(m)-f(m)> \epsilon)))$。
- 在 $R$ 上定义小于等于关系 $\le_R$ 和小于关系 $<_R$ 为，对任意的 $f,g\in B$，即对 $[f]_{\cong}\in R$ 和 $[g]_{\cong}\in R$，$[f]_{\cong}\le_R[g]_{\cong}$ 当且仅当 $f\le_B g$；$[f]_{\cong}<_R[g]_{\cong}$ 当且仅当 $f<_B g$；

## 2. 集合的等势

【集合的等势】对集合 $A$ 和 $B$，如果存在从 $A$ 到 $B$ 的双射函数，就称 $A$ 和 $B$ 等势，记作 $A\approx B$；如果不存在从 $A$ 到 $B$ 的双射函数，就称 $A$ 和 $B$ 不等式，记作 $\lnot A\approx B$。注意 $A\approx B$ 时不一定有 $A=B$，但是 $A=B$ 时一定有 $A\approx B$。

【定理】对任意的集合 $A$，有 $P(A)\approx A_2$。

【定理】对任意的集合 $A,B,C$，

- $A\approx A$
- 若 $A\approx B$，则 $B\approx A$
- 若 $A\approx B$ 且 $B\approx C$，则 $A\approx C$。

【康托定理】

- $\lnot N\approx R$
- 对任意的集合 $A$，$\lnot A\approx P(A)$

## 3. 有限集合与无限集合、集合的基数

【有限集合】集合 $A$ 是有限集合，当且仅当存在 $n\in N$，使 $n\approx A$。

【无限集合】集合 $A$ 是无限集合当且仅当 $A$ 不是有限集合，即不存在 $n\in N$ 使 $n\approx A$。

【定理】不存在与子集的真子集等势的自然数。

【推论】不存在与子集的真子集等势的有限集合。

【推论】任何与子集的真子集等势的集合均为无限集合。$N$ 和 $R$ 都是无限集合。

【推论】任何有限集合只与唯一的自然数等势。

【集合的基数】对任意的集合 $A$ 和 $B$，它们的基数分别用 $card(A)$ 和 $card(B)$ 表示，并且 $card(A) = card(B) \Leftrightarrow A\approx B$。有时把 $card(A)$ 记作 $|A|$ 或 $\#(A)$。

- 对有限集合 $A$ 和 $n\in N$，若 $A\approx n$，则 $card(A) = n$。
- 集合的基数是刻画一个集合大小（度量）的精确数学概念。可以理解为一个集合中元素个数的抽象，是有穷集合元素个数的推广。

【自然数集合 $N$ 的基数】$N$ 的基数不是自然数，因为 $N$ 不与任何自然数等势。通常把 $card(N)$ 记作 $\aleph_0$。于是 $card(Z) = card(Q) = card(N\times N) = \aleph_0$。

【实数集合 $R$ 的基数】$card(R) =\aleph_1$，因此 $card([0,1]) = card((0,1)) = card(R^+) = \aleph_1$。

## 4. 基数的算术运算、基数的比较、可数集合与连续统假设

【基数的算术运算】对任意的基数 $k,l$

- 若存在集合 $K$ 和 $L$，$K\cap L = \varnothing$，$card(K) = k$，$card(L) = l$，则 $k+l = card(K\cup L)$
- 若存在集合 $K$ 和 $L$，$card(K) = k$，$card(L) = l$，则 $k\cdot l = card(K\times L)$
- 若存在集合 $K$ 和 $L$，$card(K) = k$，$card(L) = l$，则 $k^l = card(L_K)$，其中 $L_K$ 是从 $L$ 到 $K$ 的函数的集合。

【定理】对任意的基数 $k,l,m$

- $k+l=l+k$，$k\cdot l = l\cdot k$
- $k+(l+m) = (k+l)+m$，$k\cdot(l\cdot m) = (k\cdot l)\cdot m$
- $k\cdot(l + m) = k\cdot l + k\cdot m$
- $k^{l+m} = k^l\cdot k^m$
- $(k\cdot l)^m = k^m\cdot l^m$
- $(k^l)^m = k^{(l\cdot m)}$

【基数的比较】对集合 $K$ 和 $L$，$card(K) = k$，$card(L) - l$，如果存在从 $K$ 到 $L$ 的单射函数，则称集合 $L$ 优势于 $K$，记作 $K\le L$，且称基数 $k$ 不大于基数 $l$，记作 $k\le l$。对基数 $k$ 和 $l$，如果 $k\le l$ 且 $k\ne l$，则称 $k$ 小于 $l$，记作 $k<l$。

【定理】对任意的基数 $k,l,m$

- $k\le k$
- 若 $k\le l$ 且 $l\le m$，则 $k\le m$
- 若 $k\le l$ 且 $l\le k$，则 $k=l$
- $k\le l$ 或 $l\le k$

【定理】对任意的基数 $k,l,m$，如果 $k\le l$，

- $k + m \le l + m$
- $k\cdot m\le l\cdot m$
- $k^m \le l^m$
- 若 $k\ne 0$ 或 $m\ne 0$，则 $m^k\le m^l$

【定理】对基数 $k,l$，如果 $k\le l$，$k\ne 0$，$l$ 是无限基数，则 $k+l=k\cdot l = l = \max(k,l)$

【定理】对任意的无限集合 $K$，$N\le K$；对任意的无限基数 $k$，$\aleph_0\le k$

【可数集合】对集合 $K$，如果 $card(K)\le \aleph_0$，则称 $K$ 是可数集合

- 可数集合的任何子集是可数集
- 两个可数集的并集和笛卡尔积是可数集
- 若 $K$ 是无限集合，则 $P(K)$ 是不可数的
- 可数个可数集的并集是可数集（若 $A$ 是可数集，$A$ 的元素都是可数集，则 $\cup A$ 是可数集）

【基数次序】$0,1,..,n,.., \aleph_0,\aleph_1,\aleph_2,..\aleph_i,\aleph_{i+1},..$，其中 $\aleph_{i+1} = 2^{\aleph_i}$。

【连续统假设】断言不存在基数 $k$，使 $\aleph_0 < k < 2^{\aleph_0}$。

- 连续统假设和 $ZF$ 公理系统既是独立的也是相容的。