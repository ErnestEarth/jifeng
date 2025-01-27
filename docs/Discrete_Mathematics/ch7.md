# ch7 关系

## 1. 二元关系

【有序对】由两个元素 $x$ 和 $y$（允许 $x=y$）按给定次序排列组成的二元组称为一个有序对或序偶，记作 $<x,y>$，其中 $x$ 是它的第一元素，$y$ 是它的第二元素。用集合的形式，有序对 $<x,y>$ 定义为 $<x,y> = \{\{x\}, \{x,y\}\}$。有序对 $<x,y>$ 具有以下性质：

- 当 $x\ne y$ 时，$<x,y> \ne <y,x>$；
- $<x,y> = <u,v>$ 的充要条件是 $x=u$ 且 $y=v$。

【笛卡尔积】设 $A,B$ 为集合，用 $A$ 中元素为第一元素，$B$ 中元素为第二元素构成有序对。所有这样的有序对组成的集合称为 $A$ 和 $B$ 的笛卡尔积，记作 $A\times B$。符号化表示为 $A\times B = \{<x,y> | x\in A \land y \in B\}$。

- 不适合交换律：$A\times B \ne B\times A$，其中 $A\ne B, A\ne \varnothing,B\ne \varnothing$
- 不适合结合律：$(A\times B)\times C\ne A\times(B\times C)$，其中 $A\ne \varnothing,B\ne \varnothing$
- 对于并或交运算满足分配律
- 若 $A$ 或 $B$ 中有一个为空集，则 $A\times B$ 就是空集：$A\times \varnothing = \varnothing \times B = \varnothing$
- 若 $|A| = m$，$|B| = n$，则 $|A\times B| = mn$

【二元关系】如果一个集合满足以下条件之一：

1. 集合非空，且它的元素都是有序对；
2. 集合是空集；

则称该集合为一个二元关系，记作 $R$。二元关系简称关系，对于关系 $R$，如果 $<x,y>\in R$，也可以记作 $xRy$。

【$A$ 到 $B$ 的二元关系】设 $A,B$ 为集合，$A\times B$ 的任一子集所定义的二元关系称为 $A$ 到 $B$ 的二元关系。特别地，当 $A=B$ 时，$A\times A$ 的任一子集称为 $A$ 上的一个二元关系。

- 恒等关系 $I_A = \{<x,x>|x\in A\}$
- 全域关系 $E_A = \{<x,y> | x\in A \land y\in A\}$

【定义域和值域】设 $R$ 是 $A$ 到 $B$ 的二元关系

- $R$ 中所有有序对的第一元素构成的集合称为 $R$ 的定义域，记作 $dom(R)$，形式化表示为 $dom(R) = \{x|(\exists y)(<x,y>\in R)\}$
- $R$ 中所有有序对的第二元素构成的集合称为 $R$ 的值域，记作 $ran(R)$，形式化表示为 $ran(R) = \{y |(\exists x)(x, y)\in R\}$
- $R$ 的定义域和值域的并集称为 $R$ 的域，记作 $fld(R$)，形式化表示为 $fld(R) = dom(R)\cup ran(R)$。

## 2. 关系的表示

- 集合表示法：描述法、列举法
- 关系矩阵：设集合 $X = \{x_1, x_2, .., x_m\}, Y = \{y_1,y_2,.., y_n\}$，若 $R$ 是 $X$ 到 $Y$ 的一个关系，则 $R$ 的关系矩阵是 $m\times n$ 的矩阵 $M_R$，矩阵元素是 $r_{ij}$。
- 关系图：设集合 $X = \{x_1, x_2, .., x_m\}, Y = \{y_1,y_2,.., y_n\}$，若 $R$ 是 $X$ 到 $Y$ 的一个关系，则 $R$ 的关系图是一个**有向图** $G(R) = (V,E)$，它的顶点集是 $V = X\cup Y$，边集是 $E$，从 $x_i$ 到 $y_j$ 的有向边 $e_{i,j}\in E$，当且仅当 $<x_i,y_j> \in R$。

## 3. 关系的逆、合成、限制和象

对 $X$ 到 $Y$ 的关系 $R$，$Y$ 到 $Z$ 的关系 $S$，定义

- $R$ 的逆 $R^{-1}$ 为 $Y$ 到 $X$ 的关系，显然 $(R^{-1})^{-1} = R$，$|R| = |R^{-1}|$，$M_{R^{-1}} = (M_R)^T$
- $R$ 与 $S$ 的合成 $S\circ R$（左复合）为 $X$ 到 $Z$ 的关系，$S\circ R = \{<x,y> | (\exists z)(<x,z> \in R\land <z,y> \in S)\}$，先 $R$ 后 $S$，先右后左
- 对任意的集合 $A$，定义 $R$ 在 $A$ 上的限制 $R\uparrow A$ 为 $A$ 到 $Y$ 的关系，其中 $R$ 是 $X$ 到 $Y$ 的关系，$R\uparrow A = \{<x,y> | <x,y> \in R \land x\in A\}$
- $A$ 在 $R$ 下的象 $R[A]$ 为集合 $R[A] = \{y|(\exists x)(x\in A \land <x,y>\in R\}$

**优先级：逆运算优先于其他运算，关系运算优先于集合运算**

- $dom(R^{-1}) = ran(R)$，$ran(R^{-1}) = dom(R)$
- $(R\circ S)\circ Q = R\circ (S\circ Q)$
- $(R\circ S)^{-1} = S^{-1}\circ R^{-1}$
- $fld(R) \in \cup\cup R$
- $R^0 = I_A$
- $R^{n+1} = R^n\circ R$

## 4. 关系的性质

【自反性】$\forall a\in A$，有 $<a,a>\in R$，则 $R$ 为 $A$ 上的自反关系

- 自反关系的关系矩阵的对角元素均为 $1$
- 自反关系的关系图中每个顶点都有环

【非自反性】$\forall a\in A$，有 $<a,a>\notin R$，则 $R$ 为 $A$ 上的非自反关系

- 非自反关系的关系矩阵的对角元素均为 $0$
- 非自反关系的关系图中每个顶点都没有环

【对称关系 $R$】$\forall a,b \in A$，如果 $<a,b>\in R$，则必有 $<b,a>\in R$

- 对称关系的关系矩阵是对称矩阵
- 如果两个顶点之间有边，一定是一对方向相反的边（无单边）

【反对称关系】$\forall a,b\in A$，如果 $<a,b>\in R$ 且 $<b,a>\in R$，则必有 $a=b$

- 若 $r_{ij} = 1$ 且 $i\ne j$，则 $r_{ji} = 0$
- 如果两个顶点之间有边，一定是一条有向边（无双向边）

【传递关系】$\forall a,b,c\in A$，如果 $<a,b>\in R, <b,c>\in R$，必有 $<a,c>\in R$

- 如果顶点 $a$ 能通过有向弧组成的有向路径通向顶点 $x$，则 $a$ 必须有有向弧直接指向 $x$，否则 $R$ 就不适传递的

【定理】$R$ 是 $A$ 上的关系，则

- $R$ 是自反关系的充要条件是 $I_A\subseteq R$
- $R$ 是非自反关系的充要条件是 $R\cap I_A = \varnothing$
- $R$ 是对称关系的充要条件是 $R = R^{-1}$
- $R$ 是反对称关系的充要条件是 $R\cap R^{-1} \subseteq I_A$
- $R$ 是传递关系的充要条件是 $R\circ R \subseteq R$

【关系的形式化描述】

- 自反关系：$\forall x(x\in X \to xRx)$
- 非自反关系：$\forall x(x\in X\to x\bcancel{R}x)$
- 对称关系：$\forall x\forall y(x\in X\land y \in X\land xRy \to yRx)$
- 反对称关系：$\forall x\forall y(x\in X \land y \in X \land xRy \land yRx \to x = y)$
- 传递关系：$\forall x\forall y\forall z(x\in X\land y\in X\land z\in X\land xRy\land yRz\to xRz)$

【关系的性质】设 $A$ 是集合，$R_1$ 和 $R_2$ 是 $A$ 上的关系

![关系的性质](https://gitee.com/clancisa/pictures/raw/master/%E5%85%B3%E7%B3%BB%E7%9A%84%E6%80%A7%E8%B4%A8.jpg)

![关系的性质2](https://gitee.com/clancisa/pictures/raw/master/%E5%85%B3%E7%B3%BB%E7%9A%84%E6%80%A7%E8%B4%A82.jpg)

## 5. 关系的闭包

希望已有的关系具有某些特殊的性质（如自反、对称、传递等），有些关系原本不具备这些性质，但可以通过对原关系加以扩充，使之满足这些性质，希望扩充的部分尽量小，即增加的有序对尽量少，便形成了闭包的概念。

【定理】设 $R$ 是集合 $A$ 上的关系，$m,n\in N$，$R^m\circ R^n = R^{m+n}$，$(R^m)^n = R^{mn}$。

【定理】设 $A$ 是有限集合，$|A| = n$，$R$ 是 $A$ 上的关系，则存在自然数 $s$ 和 $t$（$s\ne t$），使得 $R^s = R^t$，所有的关系数量是 $2^{n^2}$。

【定理】有限集合上关系的幂序列具有周期性：设 $A$ 是有限集合，$R$ 是 $A$ 上的关系，若存在自然数 $s$ 和 $t$（$s< t$），使得 $R^s = R^t$，则 $R^{s+k} = R^{t+k}$，$R^{s+ kp + i} = R^{s+i}$，其中 $k,i\in N$，$p = t-s$。令 $B=\{R^0,R^1,..,R^{t-1}\}$，则 $R$ 的各次幂均为 $B$ 的元素，即对任意的 $q\in N$，有 $R^q\in B$。

【闭包】设 $R$ 是非空集合 $A$ 上的关系，如果 $A$ 上有另一个关系 $R'$ 满足：

- $R'$ 是自反的（对称的或传递的）；
- $R\subseteq R'$；
- 对 $A$ 上包含 $R$ 的任何自反的（对称的或传递的）关系 $R''$（$R\subseteq R''$），有 $R'\subseteq R''$。

则称关系 $R'$ 为 $R$ 的自反（对称或传递）闭包，一般将 $R$ 的自反闭包记作 $r(R)$，对称闭包记作 $s(R)$，传递闭包记作 $t(R)$。

【闭包的性质】对非空集合 $A$ 上的关系 $R, R_1, R_2$，若 $R_1\subseteq R_2$，则

- $R$ 是自反的 $\Leftrightarrow r(R) =R$；
- $R$ 是对称的 $\Leftrightarrow s(R) = R$；
- $R$ 是传递的 $\Leftrightarrow t(R) = R$。
- $r(R_1) \subseteq r(R_2)$，$s(R_1) \subseteq s(R_2)$，$t(R_1) \subseteq t(R_2)$
- $r(R_1)\cup r(R_2) = r(R_1\cup R_2)$，$s(R_1)\cup s(R_2) = s(R_1\cup R_2)$，$t(R_1)\cup t(R_2) \subseteq t(R_1\cup R_2)$
- $rs(R) = sr(R)$，$rt(R)=tr(R)$，$st(R)\subseteq ts(R)$

【定理】$R$ 是非空集合 $A$ 上的关系，则 $r(R) = R\cup I_A$

【定理】$R$ 是非空集合 $A$ 上的关系，则 $s(R) = R\cup R^{-1}$

【定理】$R$ 是非空集合 $A$ 上的关系，则 $t(R) = R^1\cup R^2\cup ..$

【推论】设 $A$ 是非空有限集，$R$ 是集合 $A$ 上的二元关系，则存在正整数 $n$，使得 $t(R) = R\cup R^2\cup ..\cup R^n$

给定关系 $R,r(R),s(R),t(R)$ 的关系矩阵分别为 $M,M_r,M_s,M_t$，则 $M_r = M + I$，$M_s = M + M^T$，$M_t = M + M^2 + M^3 + ..$

关系图分别为 $G,G_r,G_s,G_t$，则

- 考察 $G$ 的每个顶点，如果没有环就加上一个环，最终得到的是 $G_r$
- 考察 $G$ 的每一条边，如果有一条从 $x_i$ 到 $x_j$ 的单向边，则在 $G$ 中加一条 $x_j$ 到 $x_i$ 的反方向边，最终得到的是 $G_s$
- 考察 $G$ 的每个顶点 $x_i$，找出从 $x_i$ 出发的所有 $2$ 步、$3$ 步、$..$、$n$ 步长的路径。设路径的终点为 $x_{j1},x_{j2},..,x_{jk}$。如果没有从 $x_i$ 到 $x_{ji}$ 的边，就加上这条边，最终得到 $G_t$

【定理】传递闭包的有限构造方法：$A$ 为非空有限集合，$|A| = n$，$R$ 为 $A$ 上的关系，则存在正整数 $k\le n$，使得 $t(R) = R^+ = R\cup R^2\cup ..\cup R^k$

【传递闭包的求解】图论中一个非常重要的问题，给定了一个城市的交通地图，可利用求传递闭包的方法获知任意两个地点之间是否有路相连通。

- 直接利用关系矩阵相乘来求传递闭包，在计算矩阵相乘的时候用分治法降低时间复杂度
- 利用基于动态规划的 Warshall 算法来求传递闭包

【定理】设 $X$ 是一集合，$R$ 是 $X$ 上的二元关系，则有：

- 若 $R$ 是自反的，则 $s(R),t(R)$ 也自反
- 若 $R$ 是对称的，则 $r(R),t(R)$ 也对称
- 若 $R$ 是可传递的，则 $r(R)$ 也可传递

## 6. 等价关系与划分

【等价关系】设 $R$ 为非空集合 $A$ 上的关系，如果 $R$ 是自反的、对称的和传递的，则称 $R$ 为 $A$ 上的等价关系。

- 典型等价关系：平面几何中三角形的相似关系；同学集合中的同班关系、同龄关系、同乡关系。
- 朋友关系并非等价关系，因为不满足传递性。

【等价类】设 $R$ 是非空 $A$ 集合上的等价关系，对于任何 $x\in A$，令 $[x]_R = \{y|y\in A\land xRy\}$，$[x]_R$ 是由 $x\in A$ 生成的 $R$ 等价类，$x$ 为等价类 $[x]_R$ 的表示元素。显然 $[x]_R\subseteq A$。

【定理】设 $A$ 是一个集合，$R$ 是 $A$ 上的等价关系，$xRy$ 当且仅当 $[x] = [y]$。

【定理】设 $A$ 是一个集合，$R$ 是 $A$ 上的等价关系，$\forall x,y\in A$，要么 $[x]=[y]$，要么 $[x]\cap[y] = \varnothing$。

【定理】设 $R$ 是集合 $A$ 上的等价关系，则 $A=\cup\{[x]_R|x\in A\}$。

- 由等价类的定义性质知，$X$ 内的任意两个元素对于 $R$ 的等价类或相等或分离，故 $X$ 内所有元素对 $R$ 的等价类的并集就是 $X$。也可以说，$X$ 的元素对于 $R$ 的等价类定义了 $X$ 的一个划分，且这样的划分就是唯一的。

【商集】$R$ 是 $A$ 上的等价关系，$R$ 的所有等价类构成的集合记为 $A/R:\ \{[x]_R | x\in A\}$。

【划分】给定一个非空集合 $A$，$A$ 的一个划分为非空子集族 $S = \{A_1,A_2,..,A_m\}$，满足：

- 非空子集：$\varnothing \notin S$
- 不相交：$\forall x\forall y(x,y\in S\land x\ne y \to x\cap y = \varnothing)$
- 并集为 $A$：$A_1\cup A_2\cup .. \cup A_m = A$

【等价关系与划分有一一对应关系】

- 划分到等价关系转化：$A$ 是一个非空集合，$S$ 是 $A$ 的一个划分，下述关系必定是一个等价关系：$R=\{<x,y>|x,y\in A\land x,y\ 在\ S\ 的同一个划分\}$。
- 等价关系到划分的转化：设 $A$ 是非空集合，$R$ 是 $A$ 上的等价关系，$R$ 的商集是 $A$ 的划分。

【定理】任一集合上的一个划分可产生一个等价关系，反之亦然。

【定理】等价关系诱导出的划分：对非空集合 $A$ 上的等价关系 $R$，$A$ 的商集 $A/R$ 就是 $A$ 的划分，称为由等价关系 $R$ 诱导出的 $A$ 的划分，记作 $\pi_R$。

【定理】划分 $\pi$ 诱导出的 $A$ 上的等价关系：对非空集合 $A$ 上的一个划分 $\pi$，令 $A$ 上的关系 $R_{\pi}$ 为 $R_{\pi} = \{<x,y>|(\exists z)(z\in \pi \land x\in z \land y\in z)\}$，$R_{\pi}$ 则为 $A$ 上的等价关系，称为划分 $\pi$ 诱导出的 $A$ 上的等价关系。

【定理】划分 $\pi$ 和 $A$ 上的等价关系 $R$：对非空集合 $A$ 上的一个划分 $\pi$，和 $A$ 上的等价关系 $R$，$\pi$ 诱导 $R$ 当且仅当 $R$ 诱导 $\pi$。

【Stirling 数】$n$ 个有区别的球放到 $m$ 个相同的盒子中，要求不存在空盒，其不同的方案数称为第二类 Stirling 数 $S(n,m)$：

- $S(n,0) = 0$，$S(n,1) = 1$，$S(n,n) = 1$
- $S(n,2) = 2^{n-1}-1$，$S(n,n-1) = C_n^2$
- $S(n,m) = mS(n-1,m)+S(n-1,m-1)$，$n>1$，$m\ge 1$
- $S(n,m) = \frac{1}{m!}\sum_{k=0}^m(-1)^kC_m^k(m-k)^n$

## 7. 相容关系与覆盖

【相容关系】对非空集合 $A$ 上的关系 $R$，如果 $R$ 是自反的、对称的，则称 $R$ 为 $A$ 上的相容关系。

- 关系图：每个顶点都有自回路，有向弧成对出现
- 关系矩阵：主对角线全为 $1$，矩阵关于主对角线对称

【相容类】对非空集合 $A$ 上的相容关系 $R$，若 $C\subseteq A$，且 $C$ 中任意两个元素 $x$ 和 $y$ 有 $xRy$，则称 $C$ 是由相容关系产生的相容类。形式化表示为 $C = \{x|x\in A\land(\forall y)(y\in C\to xRy)\}$

- 关系图：完全多边形的顶点的集合；任一连线上的两个顶点构成集合；任一顶点构成的单元素的集合

【最大相容类】对非空集合 $A$ 上的相容关系 $R$，一个相容类若不是任何相容类的真子集，就称为最大相容类，记作 $C_R$。

- $(\forall x)(\forall y)((x\in C_R \land y\in C_R)\to xRy)$
- $(\forall x)(x\in A - C_R\to (\exists y)(y\in C_R\land xRy))$
- 关系图：最大完全多边形的顶点的集合；任一不是完全多边形的边的连线上的两个顶点构成的集合；任一孤立点构成的单元素的集合。所谓完全多边形就是其每个顶点都与其它顶点连接的多边形。

【定理】**最大相容类的存在性**：对非空有限集合 $A$ 上的相容关系 $R$，若 $C$ 是一个相容类，则存在一个最大相容类 $C_R$，使 $C\subseteq C_R$。

【覆盖】对非空集合 $A$，若存在集合 $\Omega$ 满足 $(\forall x)(x\in \Omega\to x\subseteq A)$，$\varnothing\notin\Omega$，$\cup\Omega = A$，则称 $\Omega$ 为 $A$ 的一个覆盖，称 $\Omega$ 中的元素为 $\Omega$ 的覆盖块。

【完全覆盖】对非空集合 $A$ 上的相容关系 $R$，最大相容类的集合是 $A$ 的一个覆盖，称为 $A$ 的完全覆盖，记作 $C_R(A)$，且 $C_R(A)$ 是唯一的。

【覆盖与相容关系】对非空集合 $A$ 的一个覆盖 $\Omega = \{A_1,A_2,..A_n\}$，由 $\Omega$ 确定的关系 $R = A_1\times A_1\cup A_2\times A_2\cup .. \cup A_n\times A_n$ 是 $A$ 上的相容关系。不同的覆盖可能构造出相同的相容关系。

【定理】集合 $A$ 上相容关系 $r$ 与完全覆盖 $C_r(A)$ 存在一一对应。

注意：给定集合 $A$ 的覆盖不是唯一的，但完全覆盖是唯一的。

## 8. 偏序关系

【偏序关系】对非空集合 $A$ 上的关系 $R$，如果 $R$ 是自反的、反对称的和传递的，则称 $R$ 为 $A$ 上的偏序关系。在不会产生误解时，偏序关系 $R$ 通常记作 $\le$。当 $xRy$ 时，可记作 $x\le y$，读作 $x$ 小于等于 $y$。偏序关系又称弱偏序关系，或半序关系。

【偏序集】集合 $A$ 与 $A$ 上的关系 $R$ 一起称为一个结构。集合 $A$ 与 $A$ 上的偏序关系 $R$ 一起称为一个偏序结构，或称偏序集，并记作 $<A,R>$。例如 $<P(A), \subseteq>$ 是偏序集。

【拟序关系】对非空集合 $A$ 上的关系 $R$，如果 $R$ 是非自反的和传递的，则称 $R$ 为 $A$ 上的拟序关系。在不会产生误解时，拟序关系 $R$ 通常记作 $<$。当 $xRy$ 时，可记作 $x<y$，读作 $x$ 小于 $y$。拟序关系又称强偏序关系。

【定理】$R$ 为 $A$ 上的拟序关系，则 $R$ 是反对称的。

【定理】对 $A$ 上的拟序关系 $R$，$R\cup R^0$ 是 $A$ 上的偏序关系。

【定理】对 $A$ 上的偏序关系 $R$，$R-R^0$ 是 $A$ 上的拟序关系。

【盖住关系】对偏序集 $<A,\le>$，如果 $x,y\in A$，$x\le y$，$x\ne y$，且不存在元素 $z\in A$ 使得 $x\le z$ 且 $z \le y$，则称 $y$ 盖住 $x$。$A$ 上的盖住关系 $cov\ A$ 定义为 $cov\ A = \{<x,y>|x\in A\land y\in A\land y\ 盖住\ x\}$。

【哈斯图思路】

1. 所有顶点的自回路均省略
2. 省略所有弧上的箭头，适当排列 $A$ 中元素的位置，如 $a\le b$，则 $a$ 画在 $b$ 的下方
3. 如 $a\le b,b\le c$，则必有 $a\le c$，$a$ 到 $b$ 有边，$b$ 到 $c$ 有边，则 $a$ 到 $c$ 的无向弧省略

盖住关系的基数即哈斯图边数。

【最大元】对于偏序集 $<A,\le>$ 和集合 $A$ 的任意子集 $B$，如果存在元素 $b\in B$，使得任意 $x\in B$ 都有 $x\le b$，则称 $b$ 为 $B$ 的最大元素，简称为最大元。形式化表示为 $(\exists y)(y\in B \land(\forall x)(x\in B\to x\le y))$

【最小元】如果存在元素 $b\in B$，使得任意 $x\in B$ 都有 $b \le x$，则称 $b$ 为 $B$ 的最小元素，简称最小元。形式化表示为 $(\exists y)(y\in B \land(\forall x)(x\in B\to y\le x))$

【极大元】对于偏序集 $<A,\le>$ 和集合 $A$ 的任意子集 $B$，如果存在元素 $b\in B$，使得 $B$ 中不存在其它元素 $x$ 满足 $b \le x$，则称 $b$ 为 $B$ 的极大元素，简称为极大元。形式化表示为 $(\exists y)(y\in B \land(\forall x)((x\in B\land y \le x)\to x= y))$

【极小元】如果存在元素 $b\in B$，使得 $B$ 中不存在其它元素 $x$ 满足 $x \le b$，则称 $b$ 为 $B$ 的极小元素，简称为极小元。形式化表示为 $(\exists y)(y\in B \land(\forall x)((x\in B\land x\le y)\to x=y))$

【区别】对于偏序集 $A$ 上的子集 $B$

- $B$ 中的最小元应小于等于 $B$ 中其它各元
- $B$ 中的极小元应不大于 $B$ 中其它各元（它小于等于 $B$ 中的一些元，可与 $B$ 中另一些元无关系）
- 最小元（最大元）不一定存在，若存在必唯一
- 在非空有限集合 $B$ 中，极小元（极大元）必存在，但不一定唯一
- 极大元不一定是最大元，但最大元显然是极大元

【上界】对于偏序集 $<A,\le>$ 和集合 $A$ 的任意子集 $B$，如果存在元素 $a\in A$，使得任意 $x\in B$ 都有 $x\le a$，则称 $a$ 为子集 $B$ 的上界。形式化表示为 $(\exists y)(y\in A\land(\forall x)(x\in B\to x \le y))$

【下界】如果存在元素 $a\in A$，使得任意 $x\in B$ 都有 $a\le x$，则称 $a$ 为子集 $B$ 的下界。$(\exists y)(y\in A\land(\forall x)(x\in B\to y \le x))$

【上确界】对于偏序集 $<A,\le>$ 和集合 $A$ 的任意子集 $B$，如果存在 $B$ 的某个上界 $a$，使得对于 $B$ 的任意上界 $x$ 都有 $a\le x$，则称 $a$ 为子集 $B$ 的最小上界或上确界，记为 $sup(B) = a$。即 $B$ 的所有上界组成的集合的最小元是 $B$ 的上确界。

【下确界】如果存在 $B$ 的某个下界 $a$，使得对于 $B$ 的任意下界 $x$ 都有 $x\le a$，则称 $a$ 为子集 $B$ 的最大下界或下确界，记为 $inf(B) = a。$即 $B$ 的所有下界组成的集合的最大元是 $B$ 的下确界。

【定理】对于偏序集 $<A,\le>$ 和集合 $A$ 的任意子集 $B$

- 若 $b$ 为 $B$ 的最大元，则 $b$ 为 $B$ 的极大元、上界和上确界
- 若 $b$ 为 $B$ 的最小元，则 $b$ 为 $B$ 的极小元、下界和下确界
- 若 $a$ 为 $B$ 的上界（下界）且 $a\in B$，则 $a$ 为 $B$ 的最大元（最小元）
- 若 $B$ 有最大元（最小元），则 $B$ 的最大元（最小元）唯一
- 若 $B$ 有上确界（下确界），则 $B$ 的上确界（下确界）唯一
- 若 $B$ 为有限集，则 $B$ 的极大元、极小元恒存在

【全序关系与全序集】对偏序集 $<A,\le>$，如果对任意的 $x,y\in A$，$x$ 和 $y$ 都可比，则称 $\le$ 为 $A$ 上的全序关系，或称线序关系，称 $<A,\le>$ 为全序集。

偏序只对部分元素成立关系 $R$，全序对集合中任意两个元素都有关系 $R$。

【链】对于偏序集 $<A,\le>$，且 $B\subseteq A$，如果对任意的 $x,y\in B$，$x$ 和 $y$ 都是可比的，则称 $B$ 为 $A$ 上的链，$B$ 中元素个数称为链的长度。

【反链】如果对任意的 $x,y\in B$，$x$ 和 $y$ 都不是可比的，则称 $B$ 为 $A$ 上的反链，$B$ 中元素个数称为反链的长度。

【偏序集的分解定理】对偏序集 $<A,\le>$，设 $A$ 中最长链的长度是 $n$，则将 $A$ 中元素分成不相交的反链，反链个数至少是 $n$。换言之，设 $A$ 中最长链的长度是 $n$，$A$ 中存在 $n$ 个划分块的划分，每个划分块都是反链。

【Dilworth 定理】令 $(A,\le)$ 是一个有限偏序集，并令 $m$ 是反链的最大的大小。则 $A$ 可以被划分成 $m$ 个但不能再少的链。

【定理】对偏序集 $<A,\le>$，若 $A$ 中元素为 $mn+1$ 个，则 $A$ 中或者存在一条长度为 $m+1$ 的反链，或者存在一条长度为 $n+1$ 的链。

【良序关系与良序集】对偏序集 $<A,\le>$，如果 $A$ 的任何非空子集都有最小元，则称 $\le$ 为良序关系，称 $<A,\le>$ 为良序集。

【定理】良序集一定是全序集。

【定理】有限的全序集一定是良序集。

【良序定理】任意的有限集合都可以良序化。对每一个集合来说，都存在一种排序方法，使得它的所有子集都有极小元素。

- $<N,\le>$ 是全序集，也是良序集。$<Z,\le>$ 是全序集，但不是良序集，因为 $Z$ 无最小元。

【选择公理】我们可以从每一个在 $C$ 中的集合中，都选择一个元素和其所在的集合配成有序对来组成一个新的集合。

【佐恩引理】在任何一个非空的偏序集中，若任何链（即全序的子集）都有上界，则此偏序集内必然存在（至少一枚）极大元。

【闭区间】在全序集 $<R,\le>$ 上，对于 $a,b\in R, a\ne b, a\le b$，$[a,b] = \{x|x\in R \land a\le x\le b\}$ 称为从 $a$ 到 $b$ 的闭区间

【开区间】$(a,b) = \{x|x\in R\land a\le x\le b \land x\ne a\land x\ne b\}$ 称为从 $a$ 到 $b$ 的开区间。

【半开区间】$[a,b) = \{x|x\in R\land a\le x\le b\land x\ne b\}$，$(a,b] = \{x|x\in R\land a\le x\le b\land x\ne a\}$ 都称为从 $a$ 到 $b$ 的半开区间。

![偏序关系](img/%E5%81%8F%E5%BA%8F%E5%85%B3%E7%B3%BB.jpg)