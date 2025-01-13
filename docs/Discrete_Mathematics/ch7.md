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
- $R$ 与 $S$ 的合成 $SoR$（左复合）为 $X$ 到 $Z$ 的关系，$SoR = \{<x,y> | (\exists z)(<x,z> \in R\land <z,y> \in S)\}$，先 $R$ 后 $S$，先右后左
- 对任意的集合 $A$，定义 $R$ 在 $A$ 上的限制 $R\uparrow A$ 为 $A$ 到 $Y$ 的关系，其中 $R$ 是 $X$ 到 $Y$ 的关系，$R\uparrow A = \{<x,y> | <x,y> \in R \land x\in A\}$
- $A$ 在 $R$ 下的象 $R[A]$ 为集合 $R[A] = \{y|(\exists x)(x\in A \land <x,y>\in R\}$

**优先级：逆运算优先于其他运算，关系运算优先于集合运算**

- $dom(R^{-1}) = ran(R)$，$ran(R^{-1}) = dom(R)$
- $(RoS)oQ = Ro(SoQ)$
- $(RoS)^{-1} = S^{-1}oR^{-1}$
- $fld(R) \in \cup\cup R$
- $R^0 = I_A$
- $R^{n+1} = R^noR$

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
- $R$ 是传递关系的充要条件是 $RoR \subseteq R$

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

【定理】设 $R$ 是集合 $A$ 上的关系，$m,n\in N$，$R^moR^n = R^{m+n}$，$(R^m)^n = R^{mn}$。

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

## 6. 等价关系与划分

## 7. 相容关系与覆盖

## 8. 偏序关系

