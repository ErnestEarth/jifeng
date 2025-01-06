# ch5 谓词逻辑的等值和推理演算

## 1. 谓词逻辑的等值式

【**等值**】设 $A,B$ 是一阶谓词逻辑中任意两个公式，若 $A\leftrightarrow B$ 是普遍有效的公式，则称 $A$ 与 $B$ 等值，记作 $A=B$ 或 $A\Leftrightarrow B$。

命题公式中常常用到的等价式及永真蕴含式也可以看作是谓词演算中的等价式及永真蕴含式。

【**否定型等值式**】**否定词越过量词的移动，使用德摩根律。**

- $\lnot (\forall x) P(x) = (\exists x)\lnot P(x)$
- $\lnot (\exists x) P(x) = (\forall x)\lnot P(x)$
- $(\forall x) P(x) = \lnot (\exists x)\lnot P(x)$
- $(\exists x) P(x) = \lnot (\forall x)\lnot P(x)$

【**量词分配等值式**】

- $(\forall x) (P(x) \lor q) = (\forall x) P(x)\lor q$
- $(\exists x) (P(x) \lor q) = (\exists x) P(x)\lor q$
- $(\forall x) (P(x) \land q) = (\forall x) P(x)\land q$
- $(\exists x) (P(x) \land q) = (\exists x) P(x)\land q$
- $(\forall x) (P(x) \land q) = (\forall x) P(x)\land q$
- $(\forall x) (P(x) \to q) = (\exists x) P(x)\to q$
- $(\exists x) (P(x) \to q) = (\forall x) P(x)\to q$
- $(\forall x) (p \to Q(x)) = p \to (\forall x) Q(x)$
- $(\exists x) (p \to Q(x)) = p \to (\exists x) Q(x)$
- $(\forall x) (P(x) \land Q(x)) = (\forall x) P(x)\land (\forall x) Q(x)$
- $(\exists x) (P(x) \lor Q(x)) = (\exists x) P(x)\lor (\exists x) Q(x)$

## 2. 等值演算规则

【**置换规则**】设 $\phi(A)$ 是含公式 $A$ 的公式，若 $A\Leftrightarrow B$，则 $\phi(A) \Leftrightarrow \phi(B)$。

【**换名规则**】（约束变元换名，目的是使每个变元性质唯一）

- 设 $A$ 为一公式，将 $A$ 中某量词辖域中某约束变项的所有出现及相应的约束变元，改成该量词辖域中未曾出现过的某个体变项符号，公式中其余部分不变，设所得公式为 $A'$，则 $A'\Leftrightarrow A$。

【**代替规则**】（自由变元的代替）

- 设 $A$ 为一公式，将 $A$ 中某个自由出现的个体变项的所有出现用 $A$ 中未曾出现过的个体变项符号代替，$A$ 中的其余部分不变，设所得公式为 $A'$，则 $A'\Leftrightarrow A$。

## 3. 范式

【**前束范式**】设 $A$ 为一阶谓词逻辑公式，如果满足

1. 所有量词都位于该公式的最左边；
2. 所有量词前都不含否定词；
3. 量词的辖域都延伸到整个公式的末端，则称 $A$ 为前束范式。

前束范式的一般形式为 $(Q_1x_1)(Q_2x_2)..(Q_nx_n)M(x_1,x_2,..x_n)$，其中 $Q_i\ (1 \le i \le n)$ 为 $\forall$ 或 $\exists$，$M$ 为不含量词的公式，称作公式 $A$ 的基式或母式。

【**前束范式存在定理**】一阶谓词逻辑的任一公式都存在与之等值的前束范式，但其前束范式并不唯一。

【化前束范式的基本步骤】

1. 消去联结词蕴含和双蕴涵；
2. 否定词右移（利用否定型等值式和德摩根律）；
3. 量词左移（使用量词分配等值式）；
4. 变元易名（使用变元易名分配等值式）。

【**SKOLEM 标准型**】一阶谓词逻辑的任一公式 $A$，若其前束范式中所有的存在量词都在全称量词的左边，且至少有一个存在量词（**$\exists$ 前束范式**）；或仅保留全称量词而消去存在量词，便得到公式 $A$ 的 SKOLEM 标准型（**$\forall$ 前束范式**）。公式 $A$ 与其 SKOLEM 标准型**只能保持某种意义下的等值**关系。

【**$\forall$ 前束范式存在定理**】一阶谓词逻辑的任一公式 $A$ 都可化成相应的 $\forall$ 前束范式，并且 $A$ 是不可满足的当且仅当其 $\forall$ 前束范式是不可满足的。这种标准型对使用归结法的定理证明来说是重要的。

【**$\exists$ 前束范式存在定理**】一阶谓词逻辑的任一公式 $A$ 都可化成相应的 $\exists$ 前束范式，并且 $A$ 是普遍有效的当且仅当其 $\exists$ 前束范式是普遍有效的。

## 4. 基本推理公式

在一阶谓词逻辑中，从前提 $A_1,A_2,..A_n$ 出发推出结论 $B$ 的推理形式结构，依然采用如下的蕴含式形式：$A_1\land A_2\land..\land A_n \to B$。若该式为永真式，则称推理正确，否则称推理不正确。于是，在一阶谓词逻辑中判断推理是否正确便归结为判断上式是否为永真式，并称**满足永真式的蕴含式**为推理公式。用如下形式的符号表示：$A_1\land A_2\land..\land A_n \Leftrightarrow B$。

【**基本推理公式**】

- $(\forall x)P(x)\lor (\forall x)Q(x)\Rightarrow (\forall x)(P(x)\lor Q(x))$
- $(\exists x)(P(x)\land Q(x))\Rightarrow (\exists x)P(x)\land (\exists x) Q(x)$
- $(\forall x)(P(x)\to Q(x))\Rightarrow (\forall x)P(x)\to (\forall x)Q(x)$
- $(\forall x)(P(x)\to Q(x))\Rightarrow (\exists x)P(x)\to (\exists x)Q(x)$
- $(\forall x)(P(x)\leftrightarrow Q(x))\Rightarrow (\forall x)P(x)\leftrightarrow (\forall x)Q(x)$
- $(\forall x)(P(x)\leftrightarrow Q(x))\Rightarrow (\exists x)P(x)\leftrightarrow (\exists x)Q(x)$
- $(\forall x)(P(x)\to Q(x))\land (\forall x)(Q(x) \to R(x))\Rightarrow (\forall x)(P(x)\to R(x))$
- $(\forall x)(P(x)\to Q(x))\land P(a) \Rightarrow Q(a)$
- $(\forall x)(\forall y)P(x,y)\Rightarrow (\exists x)(\forall y)P(x,y)$
- $(\exists x)(\forall y)P(x,y)\Rightarrow (\forall y)(\exists x)P(x,y)$

## 5. 推理演算

在命题逻辑中，引入几条推理规则，配合基本推理公式所进行的推理演算方法，可以容易地推广到谓词逻辑中。由于在谓词逻辑中**不能使用真值表法**，又不存在判别 $A\to B$ 是普遍有效的一般方法，从而使用推理规则的推理方法已成为谓词逻辑的基本推理演算方法。

【**全称量词消去规则 UI**】$\frac{(\forall x)P(x)}{\therefore P(y)}$ 或 $\frac{(\forall x)P(x)}{\therefore P(c)}$，成立条件为

- 第一式中，取代 $x$ 的 $y$ 应为任意的**不在** $P(x)$ 中约束出现的个体变项。（$y$ 代表任意一个个体）
- 第二式中，$c$ 为任意个体常项。
- 用 $y$ 或 $c$ 去取代 $P(x)$ 中自由出现的 $x$ 时，必须在 $x$ 自由出现的一切地方进行取代。
- 当 $P(x)$ 中不再含有量词和其它变元时没有问题，如果允许 $P(x)$ 中含有量词和其它变元时，须限制 $y$ 不在 $P(x)$ 中约束出现。

【**全称量词引入规则 UG**】$\frac{P(y)}{\therefore(\forall x) P(x)}$，成立条件为

- 无论 $P(y)$ 中自由出现的个体变项 $y$ 取何值，$P(y)$ 应该均为真。
- 取代自由出现的 $y$ 的 $x$ 也不能在 $P(y)$ 中约束出现。

【**存在量词消去规则 EI**】$\frac{(\exists x)P(x)}{\therefore P(c)}$，成立条件为

- $c$ 是使 $P$ 为真的特定的个体常项。
- $c$ 不在 $P(x)$ 中出现。
- $P(x)$ 中没有其它自由出现的个体变项。

【**存在量词引入规则 EG**】$\frac{P(c)}{\therefore (\exists x) P(x)}$，成立条件为

- $c$ 是特定的个体常项。
- 取代 $c$ 的 $x$ 不在 $P(c)$ 中出现过。

【使用推理规则的推理演算过程】首先将以自然语句表示的推理问题引入谓词加以形式化；若不能直接使用基本的推理公式则消去量词；在无量词的条件下使用规则和公式推理；最后再引入量词以求得结论。

## 6. 归结推理

【出发点】使用推理规则的证明技巧性较强，不便于机器实现。命题逻辑中的归结推理法可以推广到谓词逻辑中。

【归结推理步骤】

1. 欲证 $A_1\land A_2\land ..\land A_n \to B$ 是定理，等价于证 $G = A_1 \land A_2 \land .. \land A_n \land \lnot B$ 是矛盾式。
2. 将 $G$ 化为前束范式，进而化为 SKOLEM 标准型，消去存在量词，得到仅含全称量词的前束范式 $G^*$。由于全称量词的前束范式 $G^*$ 保持原式 $G$ 不可满足的特性，故 $G$ 与 $G^*$ 在不可满足的意义下是一致的。
3. 略去 $G^*$ 中的全称量词，$G^*$ 中的合取词 $\land$ 以逗号表示，便得到 $G^*$ 的子句集 $S$。实用中可分别求出诸 $A_i$ 与 $\lnot B$ 的子句集。
4. 对 $S$ 做归结，直至归结出空子句 $\square$。