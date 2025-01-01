# ch2 命题逻辑的等值和推理演算

## 1. 等值定理

给定两个命题公式 $A$ 和 $B$，设 $P_1$，$P_2$，$\dots$，$P_n$ 为出现于 $A$ 和 $B$ 中的所有命题变项，则公式 $A$ 和 $B$ 共有 $2^n$ 个解释。若在任一解释下，公式 $A$ 和 $B$ 的真值都想同，则称 $A$ 和 $B$ 是等值的、或称等价，记作 $A = B$ 或 $A \Leftrightarrow B$。

【**等值定理**】设 $A$，$B$ 为两个命题公式，$A = B$ 的**充要条件**是 $A \leftrightarrow B$ 为一个重言式。

等值定理的实用性之一：若证明两个公式等值，只要证明由这两个公式构成的双条件式是重言式。

等值关系满足等价关系的三个性质：

- 自反性：$A = A$
- 对称性：若 $A = B$，则 $B = A$
- 传递性：若 $A = B$，$B = C$，则 $A = C$

两个重要结论：

1. 一个命题（原命题）与它的逆否命题等值：$P\to Q = \lnot Q \to \lnot P$
2. 一个命题的逆命题与它的否命题等值：$Q\to P = \lnot P \to \lnot Q$

## 2. 等值公式

若 $X$ 是合式公式 $A$ 的一部分，且 $X$ 本身也是一个合式公式，则称 $X$ 为公式 $A$ 的子公式。

【**置换规则**】设 $X$ 为公式 $A$ 的子公式，用与 $X$ 等值的公式 $Y$ 将 $A$ 中的 $X$ 施以代换，称为置换。

置换后公式 $A$ 化为公式 $B$，置换规则的性质保证公式 $A$ 与公式 $B$ 等值，即 $A = B$。且当 $A$ 是重言式时，置换后的公式 $B$ 也是重言式。此为**等值定律**。

【**定理**】设 $\phi(A)$ 是含命题公式 $A$ 的命题公式，$\phi(B)$ 是用命题公式 $B$ 置换了 $\phi(A)$ 中的 $A$ 之后得到的命题公式。如果 $A = B$，则 $\phi(A) = \phi(B)$。

1. 双重否定律：$\lnot \lnot P = P$

2. 结合律：

    - $(P \lor Q) \lor R = P \lor (Q \lor R)$

    - $(P \land Q) \land R = P \land (Q \land R)$

    - $(P \leftrightarrow Q) \leftrightarrow R = P \leftrightarrow (Q \leftrightarrow R)$

    - <p style="color: red;">$(P \to Q) \to R \ne P \to (Q \to R)$</p>

3. 交换律：

    - $P \lor Q = Q \lor P$

    - $P \land Q = Q \land R$

    - $P \leftrightarrow Q = Q \leftrightarrow P$

    - <p style="color: red;">$P \to Q \ne Q \to P$</p>

4. 分配律：

    - $P \lor (Q \land R) = (P \lor Q)\land (P \lor R)$

    - $P\land (Q \lor R) = (P \land Q)\lor (P \land R)$

    - $P \to (Q \to R) = (P \to Q) \to (P \to R)$

    - <p style="color: red;">$P \leftrightarrow (Q \leftrightarrow R) \ne (P \leftrightarrow Q) \leftrightarrow (P \leftrightarrow R)$</p>

5. 幂等律（恒等律）

    - $P \lor P = P$
    - $P \land P = P$
    - $P \to P = 1$
    - $P \leftrightarrow P = 1$

6. 吸收律

    - $P \lor (P \land Q) = P$
    - $P \land (P \lor Q) = P$

7. 德摩根律

    - $\lnot (P \lor Q) = \lnot P \land \lnot Q$
    - $\lnot (P \land Q) = \lnot P \lor \lnot Q$

    对蕴涵词、双条件词作否定有：

    - $\lnot (P \to Q) = P \land \lnot Q$
    - $\lnot (P \leftrightarrow Q) = \lnot P \leftrightarrow Q = P \leftrightarrow \lnot Q = (\lnot P \land Q)\lor (P \land \lnot Q)$

8. 同一律

    - $P \lor 0 = P$
    - $P \land 1 = P$
    - $1 \to P = P$
    - $1 \leftrightarrow P = P$
    - $P \to 0 = \lnot P$
    - $0 \leftrightarrow P = \lnot P$

9. 零律

    - $P \lor 1 = 1$
    - $P \land 0 = 0$
    - $P \to 1 = 1$
    - $0 \to P = 1$

10. 补余律

    - $P \lor \lnot P = 1$
    - $P \land \lnot P = 0$
    - $P \to \lnot P = \lnot P$
    - $\lnot P \to P = P$
    - $P \leftrightarrow \lnot P = 0$

**常用等值公式**：

- 蕴涵等值式：$P \to Q = \lnot P \lor Q$
- 前提合取合并：$P \to (Q \to R) = (P \land Q) \to R$
- 等价等值式：$P \leftrightarrow Q = (P \to Q) \land (Q \to P)$
- 假言易位：$P \to Q = \lnot Q \to \lnot P$
- 等价否定等值式：$P \leftrightarrow Q = \lnot P \leftrightarrow \lnot Q$
- 归谬论：$(P \to Q) \land (P \to \lnot Q) = \lnot P$
- 前提析取合并：$(P \to R) \land (Q \to R) = (P \lor Q) \to R$
- 前提交换：$P \to (Q \to R) = Q \to (P \to R)$
- $P \leftrightarrow Q = (P \land Q) \lor (\lnot P \land \lnot Q)$
- $P \leftrightarrow Q = (P \lor \lnot Q) \land (\lnot P \lor Q)$

## 3. 命题关系与真值表的关系

从取 $1$ 的行来写，行内用 $\land$，行间用 $\lor$，保持原有真值。

从取 $0$ 的行来写，行内用 $\lor$，行间用 $\land$，原有真值取反。（德摩根律）

## 4. 联结词的完备集

- 与非联结词：$\uparrow$​

    $P \uparrow Q = \lnot (P \land Q)$，当且仅当 $P$ 和 $Q$ 的真值都是 $1$ 时，$P \uparrow Q$ 的真值为 $0$。

- 或非联结词：$\downarrow$​​

    $P \downarrow Q = \lnot (P \lor Q)$，当且仅当 $P$ 和 $Q$ 的真值都是 $0$ 时，$P \downarrow Q$ 的真值为 $1$。

- 异或联结词：$\oplus$

    $P \oplus Q = (\lnot P \land Q) \lor (P \land \lnot Q)$，当且仅当 $P$ 和 $Q$ 的真值不相同时，$P \oplus Q$ 的真值为 $1$。

【真值函项】对所有的合式公式加以分类，将等值的公式视为同一类，从中选一个作代表称之为**真值函项**。每一个真值函项就有一个联结词与之对应。

$C$ 是一个联结词的集合，如果任何 $n$ 元真值函项都可以由仅含 $C$ 中的联结词构成的公式表示，则称 $C$ 是完备的联结词集合，或说 $C$​ 是联结词的**完备集**。

$\{\lnot, \lor, \land\}$ 是完备的联结词集合。

## 5. 对偶式

将给定的**仅包含 $\land$，$\lor$，$\lnot$ 联结词的**命题公式 $A$ 中出现的 $\lor$，$\land$，$1$，$0$ 分别以 $\land$，$\lor$，$0$，$1$ 代换，得到公式 $A^*$，则称 $A^*$ 是公式 $A$ 的对偶式，或者说 $A$ 和 $A^*$ 互为对偶式。

记 $A = A(P_1, P_2, \dots, P_n)$，$A^- = A(\lnot P_1, \lnot P_2, \dots, \lnot P_n)$，则有如下定理：

【定理 $1$】$\lnot(A^*) = (\lnot A)^*$，$\lnot (A^-) = (\lnot A)^-$

【定理 $2$】$(A^*)^* = A$，$(A^-)^- = A$

【定理 $3$】$\lnot A = A^{*-} = A^{-*}$

【定理 $4$】（对偶原理）若 $A = B$，必有 $A^* = B^*$

【定理 $5$】若 $A \to B$ 永真，必有 $B^* \to A^*$ 永真

【定理 $6$】$A$ 与 $A^-$ 同永真，同可满足；$\lnot A$ 与 $A^*$ 同永真，同可满足。

【定理 $7$】若 $A$ 为重言式，则 $A^*$ 必为矛盾式。

## 6. 范式

1. 文字与互补对：命题变项及其否定式（如 $P$ 与 $\lnot p$）统称文字，且 $P$ 与 $\lnot P$ 称为互补对。

2. 合取式：由文字的合取所组成的公式称为合取式。

    设 $A_i$ 是含 $n$ 个文字的简单合取式，且 $A_i$ 为矛盾式，则 $A_i$ 中必同时含某个命题变项和它的否定式，反之亦然。

    【定理】一个简单合取式是矛盾式当且仅当它同时含有某个命题变项及它的否定式（一个互补对）。

3. 析取式：由文字的析取所组成的公式称为析取式。

    设 $A_i$ 是含 $n$ 个文字的简单析取式，若 $A_i$ 中既含某个命题变项 $P_j$，又含它的否定式 $\lnot P_j$，即 $P_j \lor \lnot P_j$，则 $A_i$ 为重言式。反之，若 $A_i$ 为重言式，则它必同时含某个命题变项和它的否定式。

    【定理】一个简单析取式是重言式当且仅当它同时含有某个命题变项及它的否定式（一个互补对）。

4. 析取范式：形如 $A_1 \lor A_2 \lor \dots \lor A_n$ 的公式，其中 $A_i$ 为合取式。

5. 合取范式：形如 $A_1 \land A_2 \land \dots \land A_n$ 的公式，其中 $A_i$ 为析取式。

【范式存在定理】任一命题公式都存在与之等值的合取范式和析取范式，但命题公式的合取范式和析取范式并不唯一。

【主范式】：

- 极小项：$n$ 个命题变项组成的合取范式中，每个命题变项与它的否定式**不同时出现**，但二者之一必出现且仅出现一次，称为合取式的极小项，以 $m_i$ 表示。
    - $n$ 个命题有 $2^n$ 个极小项，彼此不等价。
    - 任一极小项只有一种指派使其取值为真，每种指派对应的一个 $n$ 位二进制数，转换为十进制数为 $i$。
    - 极小项两两不等值，且 $m_i \land m_j = F(i \ne j)$。
    - 任一含有 $n$ 个命题变项的公式，都可由 $k(\le 2^n)$ 个极小项的析取来表示。$A$ 是由 $k$ 个极小项的析取来表示，剩余 $2^n-k$ 极小项的析取是 $\lnot A$。
    - 恰由 $2^n$ 个极小项的析取构成的公式必为重言式，即 $\lor_{i=0}^{2^n-1} m_i = 1$。
- 极大项：$n$ 个命题变项组成的析取范式中，每个命题变项与它的否定式**不同时出现**，但二者之一必出现且仅出现一次，称为析取式的极大项，以 $M_i$ 表示。
    - $n$ 个命题有 $2^n$ 个极大项，彼此不等价。
    - 任一极大项只有一种指派使其取值为假。
    - 极大项两两不等值，且 $M_i \lor M_j = T(i \ne j)$。
    - 任一含有 $n$ 个命题变项的公式，都可由 $k(\le 2^n)$ 个极大项的合取来表示。$A$ 是由 $k$ 个极大项的合取来表示，剩余 $2^n-k$ 极大项的合取是 $\lnot A$。
    - 恰由 $2^n$ 个极大项的合取构成的公式必为矛盾式，即 $\land_{i=0}^{2^n-1} M_i = 0$。
    - 极小项和极大项的关系：$\lnot m_i = M_{(2^n-1-i)} = M_{(i)补}$，$\lnot M_i = m_{(2^n-1-i)} = m_{(i)补}$
- 主析取范式：仅由极小项构成的析取范式称为主析取范式。任一含有 $n$ 个命题变项的公式，都存在唯一的与之等值的且仅含这 $n$ 个命题变项的主析取范式。
- 主合取范式：仅由极大项构成的合取范式称为主合取范式。任一含有 $n$ 个命题变项的公式，都存在唯一的与之等值的且仅含这 $n$ 个命题变项的主合取范式。
- 主范式之间的转换：
    - 令 $A = \lor m_{il}$，则 $\lnot A = \lnot(\lor m_{il}) = \land \lnot m_{il} = \land M_{(il)补}$，于是 $A = \land_{(\{0,1,..,2^n-1\} - \{i1,i2,..,ik\}补)}$
    - 令 $A = \land M_{il}$，则 $\lnot A = \lnot(\land M_{il}) = \lor \lnot M_{il} = \lor m_{(il)补}$，于是 $A = \lor_{(\{0,1,..,2^n-1\} - \{i1,i2,..,ik\}补)}$
- 永真式的主合取范式为空公式，矛盾式的主析取范式为空公式。
- 主析取范式的用途
    - 求公式的成真赋值与成假赋值：若 $A$ 的主析取范式含 $s$ 个极小项，则 $A$ 有 $s$ 个成真赋值，其余 $2^n - s$ 个赋值都是成假赋值。
    - 判断公式的类型：$A$ 为重言式当且仅当 $A$ 的主析取范式含全部 $2^n$ 个极小项；$A$ 为矛盾式当且仅当 $A$ 的主析取范式不含任何极小项；$A$ 为可满足式当且仅当 $A$ 的主析取范式中至少含一个极小项。
    - 判断两个命题公式是否等值
    - 解决实际问题。

## 7. 推理形式与基本推理公式

【推理形式】将以自然语句描述的推理关系引入符号，抽象化并以条件式的形式表示出来得到推理形式，推理形式由前提和结论部分组成。前提真，结论必真的推理形式为正确的推理形式。

【重言蕴含】给定两个公式 $A,B$，如果当 $A$ 取值为真时，$B$ 就必取值为真，便称 $A$ 重言（永真）蕴含 $B$，或称 $B$ 是 $A$ 的逻辑推论，用符号 $A \Rightarrow B$ 表示。注意 $\Rightarrow$ 不是逻辑联结词，$A\Rightarrow B$ 不同于 $A\to B$。

【重言蕴含的结果】

- 如果 $A\Rightarrow B$ 成立，若 $A$ 为重言式，则 $B$ 也是重言式。
- 若 $A\Rightarrow B$ 且 $B\Rightarrow A$ 同时成立，必有 $A = B$；反之亦然。
- 若 $A \Rightarrow B$ 且 $B\Rightarrow C$ 同时成立，则有 $A\Rightarrow C$。
- 若 $A \Rightarrow B$ 且 $A\Rightarrow C$ 同时成立，则有 $A\Rightarrow B\land C$。
- 若 $A \Rightarrow C$ 且 $B\Rightarrow C$ 同时成立，则有 $A\lor B \Rightarrow C$。

【定理】

- $A\Rightarrow B$ 成立的充分必要条件是 $A \to B$ 为重言式。
- $A\Rightarrow B$ 成立的充分必要条件是 $A \land \lnot B$ 为矛盾式。

注意 $A\Rightarrow B$ 中 $A$ 自身不能必假。若 $A$ 永假，则 $A\to B$ 永真，虽然 $A\Rightarrow B$ 也成立，但没有意义。

【基本推理公式】

- $P\land Q\Rightarrow P$
- $P \Rightarrow P\lor Q$
- $P\land(P\to Q) \Rightarrow Q$
- $(P\to Q)\land(Q\to R)\Rightarrow P\to R$

## 8. 推理演算

【出发点】直观地看出由前提 $A$ 到结论 $B$ 的推演过程，且便于在谓词逻辑中使用。

【主要推理规则】

- 前提引入规则：推理过程中可随时引入前提
- 结论引入规则：中间结论可作为后续推理的前提
- 代入规则：仅限于重言式中的命题变项
- 置换规则：利用等值公式对部分公式进行置换
- 分离规则：由 $A$ 及 $A\to B$ 成立，可将 $B$ 分离出来
- 条件证明规则：$A_1\land A_2 \Rightarrow B$ 与 $A_1\Rightarrow A_2\to B$ 等价（前提引入与附加前提引入）

## 9. 归纳推理

【出发点】基于推理规则的方法，规则与公式较多，技巧较高，能否仅建立一条推理规则，便于机器证明与程序实现。

【理论依据】$A\Rightarrow B$ 成立的充分必要条件是 $A \land \lnot B$ 为矛盾式。

【归结法步骤】

1. 从 $A\land \lnot B$ 出发（欲证 $A\Rightarrow B$，等价于证明 $A\land \lnot B$ 是矛盾式）
2. 建立子句集 $S$，将 $A\land\lnot B$ 化成合取范式 $C_1\land C_2\land .. \land C_n$，其中 $C_i$ 为析取式。由 $C_i$ 构成子句集 $S = \{C_1, C_2,.. C_n\}$
3. 对 $S$ 中的子句做归结（消互补对），归结结果（归结式）仍放入 $S$ 中，重复此步
4. 直至归结出矛盾式（$\square$）