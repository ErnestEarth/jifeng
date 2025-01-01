# ch3 命题逻辑的公理化

为什么要建立或引入命题逻辑的公理系统？

- 重言式是命题逻辑研究的重点。
- 重要的重言式是逻辑规律。
- 如何掌握这些逻辑规律，以便从整体上理解和掌握命题逻辑，而不仅仅停留在对部分公式所作的直观解释性的讨论上。
- 需要系统、全面、严谨地研究等值式和推理式。
- 需要掌握重言式所揭示的逻辑规律的全体，将它们作为一个整体来考虑。

## 1. 公理系统的结构

【公理系统】从一些公理出发，根据演绎规则推导出一系列定理，这样形成的演绎体系叫作公理系统。公理系统自成体系，是一个抽象符号系统，又称之为形式系统。

【欧几里得几何学公理系统】该公理体系由五条公设和五组公理构成。公理是在任何数学学科里都适用的不需要证明的基本原理。公设是几何学里的不需要证明的基本原理，就是现代几何学里的公理。

【命题逻辑的公理系统】命题演算的重言式可组成一个严谨的公理系统，它是从一些作为初始命题的重言式（公理）出发，应用明确规定的推理规则，进而推导出一系列重言式（定理）的演绎体系。**命题逻辑的公理系统是一个抽象符号系统，不再涉及到真值**。

【公理系统的结构】

1. 初始符号：公理系统内允许出现的全体符号的集合。
2. 形成规则：公理系统内允许出现的合法符号序列的形成方法与规则。
3. 公理：精选的最基本的重言式，作为推演其它所有重言式的依据。
4. 变形规则：公理系统所规定的推理规则。
5. 建立定理：所有的重言式和对它们的证明。

## 2. 罗素公理系统

1. 初始符号

    - $A,B,C,..$（大写英文字母，表示命题）
    - $\lnot, \lor$（联结词）
    - $()$（圆括号）
    - $\vdash$（断言符），写在公式前，如 $\vdash A$ 表示 $A$ 是所要肯定的，或者说 $A$ 是永真式。

2. 形成规则

    - 符号 $\pi$ 是合式公式（$\pi$ 为命题）
    - 若 $A,B$ 是合式公式，则 $(A\lor B)$ 是合式公式
    - 若 $A$ 是合式公式，则 $\lnot A$ 是合式公式
    - 只有符号上述规则的符号序列才是合式公式

3. 定义

    - $(A\to B)$ 定义为 $(\lnot A \lor B)$
    - $(A\land B)$ 定义为 $\lnot(\lnot A \lor \lnot B)$
    - $(A\leftrightarrow B)$ 定义为 $(A\to B)\land (B\to A)$

4. 公理

    - 【公理 $1$】$\vdash ((P\lor P)\to P)$（重言律）
    - 【公理 $2$】$\vdash (P\to (P\lor Q))$（$\lor$ 引入律）
    - 【公理 $3$】$\vdash ((P\lor Q)\to (Q\lor P))$
    - 【公理 $4$】$\vdash((Q\to R)\to((P\lor Q)\to(P \lor R)))$

5. 变形（推理）规则

    - **代入规则**：如果 $\vdash A$，那么 $\vdash A \frac{\pi}{B}$（将合式公式 $A$ 中出现的符号 $\pi$ 处处都代以合式公式 $B$）
    - **分离规则**：如果 $\vdash A$，$\vdash A\to B$，那么 $\vdash B$
    - **置换规则**：定义的左右两边可互相替换。设公式 $A$，替换后为 $B$，则如果 $\vdash A$，那么 $\vdash B$。

6. 定理的推演

    定理的证明必须依据公理或已证明的定理，同时证明的过程（符号的变换过程）必须依据变形规则。

## 3. 公理系统的完备性和演绎定理

【公理系统的完备性】是否所有的重言式或所有成立的定理都可由所建立的公理系统推导出来。形象地说，完备性是指所建立的系统所能推演出的定理少不少。

【公理系统的可靠性】非重言式或不成立的公式是否也可以由所建立的公理系统推导出来。形象地说，可靠性是指所建立的系统所能推演出的定理多不多。不具备可靠性的系统是不能使用的。

命题逻辑的公理系统具有以下性质：

- **语义完全性（公理系统的完备性）**：任一重言式在命题逻辑的公理系统中都是可证的，即重言式是定理。
- **语义无矛盾性（相容性）**：公理系统必须不含有矛盾。
- **命题演算的可判定性**：任给一个公式，存在一种机械的方法在有穷步内判定该公式是否为定理。

## 4. 王浩算法：定理证明自动化系统

1. 初始符号

    - $A,B,C,..$（大写英文字母，表示命题）
    - $\lnot, \land, \lor, \to, \leftrightarrow$（联结词）
    - $\alpha, \beta, \gamma..$（希腊字母，表示公式串）

2. 定义

    - 相继式：如果 $\alpha, \beta$ 是公式串，称 $\alpha \xrightarrow{s} \beta$ 为相继式，其中 $\alpha$ 为前件，$\beta$ 为后件
    - 前件中的逗号表示 $\land$，后件中的逗号表示 $\lor$
    - $\alpha \xrightarrow{s} \beta$ 为真，记为 $\alpha\ s\Rightarrow \beta$

3. 公理

    - 如果公式串 $\alpha, \beta$ 的公式都只是命题变项 $A,B,..$，$\alpha\ s\Rightarrow \beta$ 是公理（为真）的充分必要条件是 $\alpha$ 和 $\beta$ 中至少含有一个相同的命题变项

4. 变形（推理）规则

    - **前件规则**
        - $\lnot\Rightarrow$：如果 $\alpha, \beta\ s\Rightarrow X, \gamma$，那么 $\alpha, \lnot X, \beta\ s\Rightarrow \gamma$
        - $\land\Rightarrow$：如果 $X,Y,\alpha, \beta\ s\Rightarrow \gamma$，那么 $\alpha, X\land Y, \beta\ s\Rightarrow \gamma$
        - $\lor\Rightarrow$：如果 $X, \alpha, \beta\ s\Rightarrow \gamma$ 且 $Y, \alpha, \beta\ s\Rightarrow \gamma$，那么 $\alpha, X \lor Y, \beta\ s\Rightarrow \gamma$
        - $\to\Rightarrow$：如果 $Y, \alpha, \beta\ s\Rightarrow \gamma$ 且 $\alpha, \beta\ s\Rightarrow X, \gamma$，那么 $\alpha, X\to Y, \beta\ s\Rightarrow \gamma$
        - $\leftrightarrow \Rightarrow$：如果 $X,Y,\alpha, \beta\ s\Rightarrow \gamma$ 且 $\alpha, \beta\ s\Rightarrow X, Y, \gamma$，那么 $\alpha, X\leftrightarrow Y, \beta\ s\Rightarrow \gamma$
    - **后件规则**
        - $\Rightarrow\lnot$：如果 $X, \alpha\ s\Rightarrow \beta, \gamma$，那么 $\alpha\ s\Rightarrow \beta, \lnot X, \gamma$
        - $\Rightarrow\land$：如果 $\alpha\ s\Rightarrow X,\beta, \gamma$ 且 $\alpha\ s\Rightarrow Y, \beta, \gamma$，那么 $\alpha\ s\Rightarrow \beta, X\land Y, \gamma$
        - $\Rightarrow\lor$：如果 $\alpha\ s\Rightarrow X, Y, \beta, \gamma$，那么 $\alpha\ s\Rightarrow \beta, X\lor Y, \gamma$
        - $\Rightarrow\to$：如果 $X, \alpha\ s\Rightarrow Y, \beta, \gamma$，那么 $\alpha\ s\Rightarrow \beta, X\to Y, \gamma$
        - $\Rightarrow\leftrightarrow$：如果 $X, \alpha\ s\Rightarrow Y, \beta, \gamma$ 且 $Y, \alpha\ s\Rightarrow X, \beta, \gamma$，那么 $\alpha\ s\Rightarrow \beta, X\leftrightarrow Y, \gamma$

5. 定理的推演

    定理推演的过程将所要证明的定理写成相继式形式；然后反复使用变形规则，消去全部联结词以得到一个或多个无联结词的相继式；若所有无联结词的相继式都是公理，则定理得证，否则定理不成立。