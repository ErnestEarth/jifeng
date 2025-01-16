# ch6 集合

## 1. 集合的概念与表示方法

【**集合的概念**】集合是一些确定的、可以区分的事物汇聚在一起组成的一个整体。组成一个集合的每个事物称为该集合的一个元素。

【**集合的描述性定义**】

- 集合的元素可以是任何事物
- 各个元素可以区分，不重复（互异性）
- 各个元素之间无次序（无序性）
- 任何事物是否属于一个集合，结论是确定的（确定性）

【**规定**】一个集合自身不能作为它的元素。即对任何集合 $A$ 都有 $A \notin A$。

【**外延表示法**】穷举法或列举法。

【**内涵表示法**】

- 描述法，概括法，谓词表示法，即用谓词来概括集合中元素的性质。一般而言，如果 $P(x)$ 表示一个谓词，则可以用 $\{x | P(x)\}$ 或 $\{x : P(x)\}$ 表示一个集合。
- 归纳定义法：$G = \{x | x=1 \lor (\exists y)(y \in G \land x = \{y\})\}$

【**重要结论**】集合论不能研究**由所有集合组成的集合**。

## 2. 集合间的关系与特殊集合

【**集合的相等**】两个集合 $A,B$ 相等，当且仅当它们具有相同的元素。则记作 $A=B$；否则记作 $A\ne B$。该定义的符号化表示为

- $A=B \Leftrightarrow (\forall x) (x\in A \leftrightarrow x \in B)$
- $A\ne B \Leftrightarrow (\exists x) \lnot (x\in A \leftrightarrow x \in B)$

【**子集**】设 $A,B$ 为集合，若 $A$ 中的每个元素都是 $B$ 的元素，则称 $A$ 为 $B$ 的子集合，简称子集。这时称 $B$ 包含 $A$，记作 $A \subseteq B$。该定义的符号化表示为 $A \subseteq B \Leftrightarrow (\forall x)(x \in A \to x \in B)$。

两个集合相等的充要条件是它们互为子集。符号化表示为 $A=B\Leftrightarrow (A\subseteq B \land B \subseteq A)$。

对任意的集合 $A,B$ 和 $C$，包含关系 $\subseteq$ 具有下列性质：

- 自反性：$A\subseteq A$
- 反对称性：$(A\subseteq B \land B \subseteq A)\Rightarrow A = B$
- 传递性：$(A\subseteq B \land B \subseteq C)\Rightarrow A \subseteq C$

【**真子集**】对任意两个集合 $A$ 和 $B$，若 $A\subseteq B$ 且 $A\ne B$，则称 $A$ 是 $B$ 的真子集，或称 $B$ 真包含 $A$。记作 $A\subset B$。该定义的符号化表示为 $A\subset B \Leftrightarrow(A\subseteq B \land A\ne B)$。

若两个集合 $A$ 和 $B$ 没有公共元素，就称 $A$ 和 $B$ 是不相交的。该定义也可写成 $\lnot(\exists x)(x \in A \land x \in B)$。

【**空集**】不含任何元素的集合称为空集，记作 $\varnothing$。空集可符号化为 $\varnothing =\{x | x \ne x\}$，$(\forall x)(x \notin \varnothing)$。空集是一切集合的子集。即，对任意的集合 $A$，$\varnothing \subseteq A$。

【**全集**】在给定的问题中，所考虑的所有事物的集合称为全集，记作 $E$。全集的定义可符号化表示为 $E = \{x | x = x\}$。全集是有相对性的，不同的问题有不同的全集。即使同一个问题也可以取不同的全集。

## 3. 集合的运算

【并集】$A\cup B$ 定义为 $A\cup B = \{x | x \in A \lor x \in B\}$ 

【交集】$A\cap B$ 定义为 $A\cap B = \{x | x \in A \land x \in B\}$ 

【差集】$A- B$ 定义为 $A- B = \{x | x \in A \land x \notin B\}$，也称 $B$ 对 $A$ 的相对补集

【余集】$-A$ 定义为 $-A = E - A = \{x | x \in E \land x \notin A\}$，$A$ 的余集也称 $A$ 的绝对补集，也是 $A$ 对 $E$ 的相对补集

【对称差】$A\oplus B$ 定义为 $A\oplus B = (A-B)\cup(B-A) = \{x | x \in A \triangledown x \in B\} = (A\cup B) - (A \cap B)$

【广义并】设 $A$ 为集合，$A$ 的元素也都是集合，则将 $A$ 的所有元素的元素组成的集合称为 $A$ 的广义并，记作 $\cup A$。符号化表示为 $\cup A = \{x | (\exists z)(z \in A \land x \in z)\}$。对空集可以进行广义并，$\cup \varnothing = \varnothing$。

【广义交】设 $A$ 为非空集合，$A$ 的元素也都是集合，则将 $A$ 的所有元素的**公共元素**组成的集合称为 $A$ 的广义并，记作 $\cap A$。符号化表示为 $\cap A = \{x | (\forall z)(z \in A \to x \in z)\}$。规定 $\cap \varnothing$ 不存在。

【幂集】设 $A$ 为集合，由 $A$ 的所有子集组成的集合称为 $A$ 的幂集，记作 $P(A)$。符号化表示为 $P(A) = \{x | x \subseteq A\}$。$x \in P(A) \Leftrightarrow x \subseteq A$。

【定理】设 $A$ 为一个有限集，且 $|A| = n$，则 $A$ 的子集个数为 $2^n$。

【序偶】由两个元素 $x$ 和 $y$（允许 $x=y$）按给定次序排列组成的二元组称为一个有序对或序偶，记作 $<x,y>$，其中 $x$ 是它的第一元素，$y$ 是它的第二元素。有序对 $<x,y>$ 具有以下性质：

1. 当 $x\ne y$ 时，$<x,y> \ne <y,x>$。
2. $<x,y> = <u,v>$ 的充要条件是 $x=u$ 且 $y=v$。

用集合的形式，有序对 $<x,y>$ 定义为 $<x,y> = \{\{x\}, \{x,y\}\}$。

【$n$ 元组】若 $n\in N$ 且 $n > 1$，$x_1, x_2, .., x_n$ 是 $n$ 个元素，则 $n$ 元组 $<x_1, x_2, .., x_n>$ 定义为

- 当 $n=2$ 时，二元组是有序对 $<x_1, x_2>$
- 当 $n\ne 2$ 时，$<x_1, x_2, .., x_n> = <<x_1, x_2, .., x_{n-1}>, x_n>$

【笛卡尔积】设 $A,B$ 为集合，用 $A$ 中元素为第一元素，$B$ 中元素为第二元素构成有序对。所有这样的有序对组成的集合称为 $A$ 和 $B$ 的笛卡尔积，记作 $A \times B$。符号化表示为 $A\times B = \{<x,y>|x\in A \land y \in B\}$。

【$n$ 阶笛卡尔积】若 $n\in N$ 且 $n>1$，$A_1,A_2,.., A_n$ 是 $n$ 个集合，它们的 $n$ 阶笛卡尔积记作 $A_1\times A_2\times..\times A_n$，并定义 $A_1\times A_2\times..\times A_n=\{<x_1,x_2,..,x_n> | x_1\in A_1 \land x_2 \in A_2 \land .. \land x_n\in A_n\}$

【一元运算】广义并、广义交、幂集、绝对补运算

【二元运算】并、交、对称差、笛卡尔积、相对补运算

【优先级】一元运算优先于二元运算；二元运算优先于集合关系运算；集合关系运算优先于逻辑运算；括号内优先于括号外；同一层括号内，相同优先级，按从左到右的顺序进行。

## 4. 集合运算的性质

【集合恒等式】对任意的集合 $A,B,C$，下列恒等式成立

- 交换律：$A\cup B = B \cup A$，$A\cap B = B \cap A$
- 结合律：$(A\cup B)\cup C = A\cup(B\cup C)$，$(A\cap B)\cap C = A\cap(B\cap C)$
- 分配律：$A\cup(B\cap C) = (A\cup B)\cap (A\cup C)$，$A\cap(B\cup C) = (A\cap B)\cup (A\cap C)$
- 幂等律：$A\cup A = A$，$A\cap A = A$
- 吸收律：$A\cup (A\cap B) = A$，$A\cap (A\cup B) = A$
- 德摩根律：$A-(B\cup C) = (A-B)\cap(A-C)$，$A-(B\cap C) = (A-B)\cup(A-C)$，$-(B\cup C) = -B\cap -C$，$-(B\cap C) = -B \cup - C$
- 同一律：$A\cup \varnothing = A$，$A\cap E = A$
- 零律：$A\cup E = E$，$A\cap \varnothing = \varnothing$
- 补余律：$A\cup -A = E$（排中律），$A\cap -A = \varnothing$（矛盾律）
- 补律：$-\varnothing = E$，$-E = \varnothing$
- 双补律：$-(-A) = A$

【差集的性质】对任意的集合 $A,B,C$

- $A-B = A-(A\cap B)$
- $A-B = A\cap -B$
- $A\cup (B-A) = A\cup B$
- $A\cap (B-C) = (A\cap B) - C$

【对称差的性质】对任意的集合 $A,B,C$

- 交换律：$A\oplus B = B\oplus A$
- 结合律：$(A\oplus B)\oplus C = A\oplus(B\oplus C)$
- 分配律：$A\cap (B\oplus C) = (A\cap B)\oplus(A\cap C)$
- 同一律：$A\oplus \varnothing = A$
- 零律：$A\oplus A = \varnothing$
- 吸收律：$A\oplus(A\oplus B) = B$

【包含关系的性质】对任意的集合 $A,B,C,D$

- $A\subseteq B\Rightarrow (A\cup C) \subseteq(B\cup C)$
- $A\subseteq B\Rightarrow (A\cap C) \subseteq(B\cap C)$
- $(A\subseteq B) \land (C\subseteq D)\Rightarrow (A\cup C) \subseteq(B\cup D)$
- $(A\subseteq B) \land (C\subseteq D)\Rightarrow (A\cap C) \subseteq(B\cap D)$
- $(A\subseteq B) \land (C\subseteq D)\Rightarrow (A-D) \subseteq(B-C)$
- $C\subseteq D\Rightarrow (A-D) \subseteq(A- C)$

【幂集的性质】对任意的集合 $A,B$

- $A\subseteq B\Leftrightarrow P(A) \subseteq P(B)$
- $A= B\Leftrightarrow P(A) = P(B)$
- $P(A)\in P(B)\Rightarrow A \in B$
- $P(A)\cap P(B) = P(A\cap B)$
- $P(A)\cup P(B)\subseteq P(A\cup B)$
- $P(A-B)\subseteq (P(A)-P(B))\cup \{\varnothing\}$
- 若 $x\in A$，$y \in A$，则 $<x,y> \in PP(A)$，其中 $PP(A)$ 表示 $P(P(A))$

【传递集合】如果集合 $A$ 的任一元素的元素都是 $A$ 的元素，就称 $A$ 为传递集合。符号化表示为 $(\forall x)(\forall y)((x\in y \land y \in A)\to x\in A)$。

- 若 $A$ 是传递集合，则有 $x\in A \Rightarrow x \subseteq A$，即任一传递集合的元素一定是它的子集，反之不成立。
- 对不包含本元（非集合元素）的集合 $A$，$A$ 是传递集合 $\Leftrightarrow A\subseteq P(A)$。
- 对不包含本元的集合 $A$，$A$ 是传递集合 $\Leftrightarrow P(A)$ 是传递集合。
- 对不包含本元的传递集合 $A$，有 $\varnothing \in A$。

【广义并和广义交的性质】对任意的集合 $A,B$

- $A\subseteq B \Rightarrow \cup A \subseteq \cup B$
- $A\subseteq B \Rightarrow \cap B \subseteq \cap A$
- $\cup(A\cup B) = (\cup A)\cup(\cup B)$
- $\cap(A\cup B) = (\cap A)\cap(\cap B)$，其中 $A$ 和 $B$ 非空
- $\cup(P(A)) = A$
- 若集合 $A$ 是传递集合，则 $\cup A$ 是传递集合
- 若集合 $A$ 的元素都是传递集合，则 $\cup A$ 是传递集合
- 若非空集合 $A$ 是传递集合，则 $\cap A$ 是传递集合，且 $\cap A \ne \varnothing$
- 若非空集合 $A$ 的元素都是传递集合，则 $\cap A$ 是传递集合

【笛卡尔积的性质】对任意的集合 $A,B,C$

- $A\times(B\cup C) = (A\times B)\cup (A\times C)$
- $A\times(B\cap C) = (A\times B)\cap (A\times C)$
- $(B\cup C)\times A = (B\times A)\cup (C\times A)$
- $(B\cap C)\times A = (B\times A)\cap (C\times A)$
- 若 $C\ne \varnothing$，则 $(A\subseteq B)\Leftrightarrow (A\times C\subseteq B\times C)\Leftrightarrow (C\times A\subseteq C\times B)$
- 设 $D$ 是任意集合，有 $(A\times B\subseteq C\times D)\Leftrightarrow (A\subseteq C\land B\subseteq D)$

## 5. 有限集合的基数

【有限集合的基数】如果存在 $n\in N$，使集合 $A$ 与集合 $\{x | x\in N \land x < n\} = \{0,1,2,..,n-1\}$ 的元素个数相同，就称集合 $A$ 的基数是 $n$，记作 $|A| = n$ 或 $card(A) = n$。空集的基数是 $0$。

【有限集合】如果存在 $n\in N$，使 $n$ 是集合 $A$ 的基数，就称 $A$ 是有限集合。如果不存在这样的 $n$，就称 $A$ 是无限集合。

【幂集的基数】对有限集合 $A$，$|P(A)| = 2^{|A|}$

【笛卡尔积的基数】对有限集合 $A,B$，$|A\times B| = |A|\cdot|B|$

【基本运算的基数】

- $|A\cup B| \le |A| + |B|$
- $|A\cap B| \le \min(|A|, |B|)$
- $|A-B| \ge |A| - |B|$
- $|A\oplus B| = |A| + |B| - 2|A\cap B|$

【容斥原理】对有限集合 $A$ 和 $B$，$|A\cup B| = |A| + |B| - |A\cap B|$。该定理可推广到 $n$ 个集合的情形，若 $n\in N$ 且 $n>1$，$A_1,A_2,..,A_n$ 是有限集合，则 $|A_1\cup A_2\cup .. \cup A_n|= \sum_{1\le i \le n}|A_i| - \sum_{1\le i<j\le n} |A_i\cap A_j| +\\ \sum_{1 \le i<j<k\le n}|A_i\cap A_j\cap A_k| + .. + (-1)^{n-1}|A_1\cap A_2\cap .. \cap A_n|$

$|\bar{A}| = N - |A|$，其中 $N$ 是集合 $U$ 的元素个数，即不属于 $A$ 的元素个数等于集合的全体减去属于 $A$ 的元素的个数。一般有 $|\bar{A_1}\cap \bar{A_2}\cap .. \cap \bar{A_n}|= N - |A_1\cup A_2\cup .. \cup A_n| \\
= N - \sum_{i=1}^n|A_i + \sum_{i=1}^n\sum_{j>i}|A_i \cap A_j| - \sum_{i=1}^n\sum_{j>i}\sum_{k>j}|A_i\cap A_j\cap A_k| + .. + (-1)^n|A_1\cap A_2\cap .. \cap A_n|$

## 6. 集合论公理系统

【基本思想】集合论公理系统的一个基本思想是**任一集合的所有元素都是集合**。集合论研究的对象只是集合，除集合外的其它对象（如有序对、数字、字母）都要用也完全可以用集合来定义。

【主要目的】集合论公理系统的主要目的：

- 判定集合的存在性
- 由已知集合构造出所有合法的集合（合法性）

集合论公理系统是一阶谓词公理系统的扩展，它包括一阶谓词公理系统和几个集合论公理。集合论公理系统可以推出一阶谓词的所有定理，也可以推出集合论的定理。

【ZFC 集合论公理系统的基本思想】

- 把**集合**当作整个数学的第一概念，没有定义，也不可能定义
- 建立一个一阶逻辑语言，用于精确地表达关于集合的命题

【ZFC 集合论公理系统的基本公理】

- **外延公理**：两个集合相等的充要条件是它们恰好具有相同的元素。该公理表明一个集合由其元素唯一确定。
- **空集存在定理**：存在不含任何元素的集合（空集）。该公理定义了集合论中的第一个集合 —— 空集，且由外延公理可知，空集是唯一的。
- **无序对集合存在公理**：对任意的集合 $x$ 和 $y$，存在一个集合 $z$，它的元素恰好为 $x,y$。有了该公理，便可无休止地构造许多具体的集合。
- **并集合存在公理**：对任意的集合 $x$，存在一个集合 $y$，它的元素恰好为 $x$ 的元素的元素。解决了集合的广义并的存在性，集合的广义并是集合。
- **子集公理模式（分离公理模式）**：对任意的谓词公式 $P(z)$，对任意的集合 $x$，存在一个集合 $y$，它的元素 $z$ 恰好既是 $x$ 的元素又使 $P(z)$ 为真。可解决交集、差集、广义交、广义并和笛卡尔积的存在性。
- **幂集公理（集合的幂集是集合）**：对任意的集合 $x$，存在一个集合 $y$，它的元素恰好是 $x$ 的子集。
- **正则公理**：对任意的非空集合 $x$，存在 $x$ 的一个元素，它和 $x$ 不相交。此时称该元素为集合 $x$ 的一个极小元，任一非空集合都有极小元。该公理说明**不存在以自身为元素的集合**；**不存在所有集合组成的集合**；**不存在无限递降的集合序列**。
- **无穷公理**：存在一个由所有自然数组成的集合。
- **替换公理模式**：对于任意的谓词公式 $P(x,y)$，如果对任意的 $x$ **存在唯一**的 $y$ 使得 $P(x,y)$ 为真，那么对所有的集合 $t$ 就存在一个集合 $s$，使 $s$ 中的元素 $y$ 恰好是 $t$ 中元素 $x$ 所对应的那些 $y$。
- **选择公理**：对任意的关系 $R$，存在一个函数 $F$，$F$ 是 $R$ 的子集，而且 $F$ 和 $R$ 的定义域相等。

【万有集不存在定理】不存在集合 $A$，使任一集合都是 $A$ 的元素。

【交集存在定理】对任意的集合 $A$ 和 $B$，交集 $A\cap B$ 是集合。

【差集存在定理】对任意的集合 $A$ 和 $B$，差集 $A-B$ 是集合。

【广义交存在定理】对任意的非空集合 $A$，广义交 $\cap A$ 是集合。

【笛卡尔积存在定理】对任意的集合 $A$ 和 $B$，笛卡尔积 $A\times B$ 是集合。

【集合的重要性质】

- 对任意的集合 $A$，$A\notin A$
- 对任意的集合 $A,B$，有 $\lnot(A\in B \land B \in A)$