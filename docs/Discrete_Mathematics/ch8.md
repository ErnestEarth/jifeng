# ch8 函数

## 1. 函数与选择公理

【函数的表示方法】列表法、图像法、解析法。

【函数】对集合 $A$ 到集合 $B$ 的关系 $f$，若满足 $\forall x\in dom(f)$，存在唯一的 $y\in ran(f)$，使 $xfy$ 成立，且 $dom(f) = A$，则称 $f$ 为从 $A$ 到 $B$ 的函数，或称 $f$ 把 $A$ 映射到 $B$。一个从 $A$ 到 $B$ 的函数 $f$，可以写成 $f:A\to B$。这时若 $xfy$，则可记作 $f:x|\to y$ 或 $f(x) = y$。

- 单值性：$(\forall x)(\forall y_1)(\forall y_2)((xfy_1\land xfy_2)\to y_1=y_2$，同一个 $x$ 不能对应多个 $y$，但是多个 $x$ 可以对应同一个 $y$，因此函数的逆关系不一定是函数。
- 定义域必须取遍 $A$ 中所有元素：$(\forall x)(x\in A\to (\exists y)(y\in B\land xfy))$
- 关系矩阵每行有且仅有一个 $1$，其余均为 $0$。
- 关系图上，集合 $A$ 中的每个顶点恰好发出一条有向边。

【从 $A$ 到 $B$ 的所有函数的集合】对集合 $A$ 和 $B$，从 $A$ 到 $B$ 的所有函数的集合记为 $A_B$，于是 $A_B = \{f|f:A\to B\}$。若 $A$ 和 $B$ 是有限集合，且 $|A| = m,|B|=n$，则 $|A_B| = n^m = |B|^{|A|}$。

【函数的象】设 $f:A\to B$，$A_1\subseteq A$，定义 $A_1$ 在 $f$ 下的象 $f[A_1]$ 为 $f[A_1] = \{y|(\exists x)(x\in A_1\land y = f(x))\}$，把 $f[A]$ 称为函数的象。设 $B_1\subseteq B$，定义 $B_1$ 在 $f$ 下的完全原象 $f^{-1}[B_1]$ 为 $f^{-1}[B_1] = \{x|x\in A\land f(x)\in B_1\}$。

【满射】设 $f:A\to B$，若 $ran(f) = B$，则称 $f$ 是满射的。

【单射】设 $f:A\to B$，若对任意的 $x_1,x_2\in A, x_1\ne x_2$ 都有 $f(x_1)\ne f(x_2)$，则称 $f$ 是单射的，或内射的。

【双射】设 $f: A\to B$，若 $f$ 既是满射的，又是单射的，则称 $f$ 是双射的，或一对一 $A$ 到 $B$ 上的。

【常函数】设 $f:A\to B$，如果存在一个 $y\in B$，使得对所有的 $x\in A$，有 $f(x) = y$，即有 $f[A] = \{y\}$，则称 $f:A\to B$ 为常函数。

【恒等函数】$A$ 上的恒等关系 $I_A:A\to A$ 称为恒等函数，于是，对任意的 $x\in A$，有 $I_A(x) = x$。

【单调函数】对实数集 $R$，设 $f: R\to R$，如果 $(x\le y)\to (f(x)\le f(y))$，则称 $f$ 是单调递增的；如果 $(x< y)\to(f(x)< f(y))$，则称 $f$ 为严格单调递增的。

【$n$ 元运算】对集合 $A$，$n\in N$，称函数 $f:A^n\to A$ 为 $A$ 上的 $n$ 元运算。

【泛函】设 $A,B,C$ 是集合，$B_C$ 为从 $B$ 到 $C$ 的所有函数的集合，则 $F:A\to B_C$ 称为一个泛函（有时将 $G:B_C\to A$ 称为一个泛函）。

【典型映射 / 自然映射】设 $R$ 是 $A$ 上的等价关系，令 $g:A\to A/R$，$g(a) = [a]_R$，则称 $g$ 为从 $A$ 到商集 $A/R$ 的典型映射或自然映射，其中 $A/R$ 是以 $R$ 的等价类为元素的集合。

【选择公理】对任意的关系 $R$，存在函数 $f$，使得 $f\subseteq R$ 且 $dom(f) = dom(R)$。设 $C$ 为一个由非空集合所组成的集合。那么我们可以从每一个在 $C$ 中的集合中，都选择一个元素和其所在的集合配成有序对来组成一个新的集合。

## 2. 函数的合成与函数的逆

【函数的合成】设 $g:A\to B$，$f:B\to C$，则 $f\circ g$ 是函数 $f\circ g: A\to C$，且对任意的 $x\in A$，有 $(f\circ g)(x) = f(g(x))$。

- 若 $f,g$ 是满射的，则 $f\circ g$ 是满射的。
- 若 $f,g$ 是单射的，则 $f\circ g$ 是单射的。
- 若 $f,g$ 是双射的，则 $f\circ g$ 是双射的。
- 若 $f\circ g$ 是满射的，则 $f$ 是满射的。
- 若 $f\circ g$ 是单射的，则 $g$ 是单射的。
- 若 $f\circ g$ 是双射的，则 $f$ 是满射的，$g$ 是单射的。

【定理】设 $f:A\to B$，则 $f = f\circ I_A \ I_B\circ f$

【函数的逆与反函数】若 $f:A\to B$ 是双射的，则 $f^{-1}$ 是函数，$f^{-1}: B\to A$。称 $f^{-1}:B\to A$ 为 $f$ 的反函数。且反函数 $f^{-1}:B\to A$ 是双射的。

【定理】若 $f:A\to B$ 是双射的，则对任意的 $x\in A$，有 $f^{-1}(f(x)) = x$，对任意的 $y\in B$，有 $f(f^{-1}(y)) = y$。

【左逆和右逆】设 $f:A\to B$，$g: B\to A$，如果 $g\circ f = I_A$，则称 $g$ 为 $f$ 的左逆；如果 $f\circ g = I_B$，则称 $g$ 为 $f$ 的右逆。

【定理】设 $f:A\to B$，$A\ne \varnothing$，则

- $f$ 存在左逆，当且仅当 $f$ 是单射的；
- $f$ 存在右逆，当且仅当 $f$ 是满射的；
- $f$ 存在左逆又存在右逆，当且仅当 $f$ 是双射的，且此时 $f$ 的左逆等于右逆。

## 3. 函数的性质

【函数的相容性】设 $f:A\to B$，$g:C\to D$，如果对任意的 $x\in A\cap C$，都有 $f(x) = g(x)$，就说 $f$ 和 $g$ 是相容的。

【函数集的相容性】设 $C$ 是由一些函数组成的集合，如果 $C$ 中任意两个函数 $f$ 和 $g$ 都是相容的，就说 $C$ 是相容的。

【定理】设 $f:A\to B$，$g:C\to D$，则 $f$ 和 $g$ 是相容的当且仅当 $f\cup g$ 是函数。

【定理】设 $f:A\to B$，$g:C\to D$，则 $f$ 和 $g$ 是相容的当且仅当 $f\uparrow (A\cap C) = g\uparrow (A\cap C)$。

【定理】对函数的集合 $C$，若 $C$ 是相容的，且 $F=\cup C$，则 $F$ 是函数 $F:dom(F)\to ran(F)$，且 $dom(F) = \cup\{dom(f)|f\in C\}$。相容的函数集合 $C$ 可以构造一个函数 $F$。

【关系与函数的相容性】设 $R$ 是 $A$ 上的等价关系，且 $f:A\to A$，如果对任意的 $x,y\in A$，有 $<x,y>\in R\Rightarrow <f(x),f(y)>\in R$，则称关系 $R$ 与函数 $f$ 是相容的。

【定理】设 $R$ 是 $A$ 上的等价关系，且 $f:A\to A$，如果 $R$ 与 $f$ 是相容的，则存在唯一的函数 $F:A/R\to A/R$，使 $F([x]_R) = [f(x)]_R$；如果 $R$ 与 $f$ 不相容，则不存在这样的函数 $F$。

## 4. 特征函数、模糊子集

【特征函数】设 $E$ 是全集，对任意的 $A\subseteq E$，$A$ 的特征函数 $\chi_A$ 定义为：
$$
\chi_A: E\to \{0,1\}, \chi_A(a) = 
\begin{cases}
1 & a\in A\\
0 & a\notin A
\end{cases}
$$

- $(\forall x)(\chi_A(x) = 0)\Leftrightarrow A = \varnothing$
- $(\forall x)(\chi_A(x) = 1)\Leftrightarrow A = E$
- $(\forall x)(\chi_A(x)\le \chi_B(X)) \Leftrightarrow A\subseteq B$
- $(\forall x)(\chi_A(x)= \chi_B(X)) \Leftrightarrow A= B$
- $\chi_{A\cap B}(x) = \chi_A\times \chi_B(x)$
- $\chi_{A\cup B}(x) = \chi_A(x) + \chi_B(x) - \chi_{A\cap B}(x)$
- $\chi_{A-B}(x) = \chi_A(x) - \chi_{A\cap B}(X)$
- $\chi_{-A}(x) = 1 - \chi_A(x)$

【模糊集合】如果 $E$ 是对象 $x$ 的集合，则 $E$ 上的模糊集合 $A:A = \{(x,\mu_A(x))|x\in E\}$，$\mu_A(x)$ 称为模糊集合 $A$ 的隶属函数。

【隶属函数】设 $E$ 是全集，对任意的 $A\subseteq E$，$A$ 的隶属函数 $\chi_A$ 定义为 $\chi_A: E\to \{0,1\}, \chi_A(a)\to[0,1]$。

- 隶属函数取值在 $0$ 和 $1$ 之间，其值的确定具有主观性和个人的偏好。