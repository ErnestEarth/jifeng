# ch2 决策树学习

## 1. 基本概念

- 实例空间：所有可能的属性构成实例空间。
- 假设分类：$\tt IF - THEN$ 决策。
- 训练样例：已知结果的实例及其结果构成训练样例。

假设我们有 $n$ 个 $2$ 值属性，那么实例空间的大小为 $2^n$，那么训练样本空间最大为 $2^{2^n}$。

## 2. 决策树

适用情况：

- 涉及到非数值数据
- 离散特征的学习和建模
- 没有相似的自然概念
- 无序
- 用属性列表表示，而不是向量

决策树表示：

- 非叶子结点：特征、属性
- 分支：特征或属性的取值
- 叶子结点：决策、标签
- 从根结点到叶子结点之间是合取关系
- 不同分支之间是析取关系

## 3. 经典决策树算法（CART）

经典决策树算法包括：$\tt CART$、$\tt ID3$、$\tt C4.5$。

一般步骤：

1. 用训练数据构建一棵决策树；
2. 基于训练样本集合进行分裂，即子集合划分；
3. 当子集合不可再分时停止分裂；
4. 或者子集合已经分裂到一个可接受的程度时停止分裂。

$\tt ID3$：

- 自顶向下，贪心搜索
- 递归算法
- 主流程：
    - 获取到下一步分裂**最好**的属性 $A$；
    - 将属性 $A$ 作为当前结点；
    - 对于属性 $A$ 的每一个取值，构建子孙结点；
    - 将训练样例分配到叶子结点；
    - 如果训练样本空间已经**完美分配**，则算法结束，否则重复该流程。

**最好的属性**：原则是越简单越好，即树的结点数越压缩、高度越矮越好，分类出来的数据越纯越好。

- 熵：$Entropy(N) = -\sum_j P(w_j)\log_2 P(w_j)$，用熵来描述信息的不确定性，衡量信息的纯度。 

- $\tt Gini$ 不纯度：$i(N) = \sum_{i \ne j} P(w_i)P(w_j) = 1 - \sum_j P^2(w_j)$，最大不纯度为 $1 - 1/n$。

- 错误分类不纯度：$i(N) = 1 - \max_j P(w_j)$，最大不纯度为 $1 - 1/n$。

**信息增益**：根据某个特征对数据排序整理带来的熵的期望减少量，**减少量越大越好**：$Gain(S, A) = Entropy(S) - \sum_{v \in Values(A)} \frac{|S_v|}{|S|}Entropy(S_v)$

**完美分配**：所有同一个子集合的数据具有相同的输出分类；所有同一个子集合的数据具有相同的输入值。没有信息增益的特征可能在和其他特征组合时有用，也可能没用。

决策树的假设空间：

- 假设空间是完备的
- 输出单一假设，决策树一般不要超过 $20$ 层
- 没有回溯
- 每一步都用到了所有数据，是一种基于统计的决策选择，对于数据噪声具有鲁棒性

$\tt ID3$ 中的偏倚：

- 样本空间 $H$ 是实例空间 $X$ 的幂集，对假设空间没有限制
- 偏好根部附近具有高 $IG\ (Information\ Gain)$ 属性的决策树，并尝试找出最短的树
- 偏倚是对某些假设的偏好（搜索偏倚），而不是对假设空间的限制（语言偏倚）

## 4. 过拟合和剪枝

**过拟合**：假设 $h\in H$，目前有一个新数据 $h' \in H$，如果 $err_{train}(h) < err_{train}(h')$ 并且 $err_{test}(h) > err_{test}(h')$，此时 $h$ 发生了过拟合。比如每一个叶子上只有一个训练样例，那么对于新数据就会出现无法匹配的情况。

**处理方法**：

- 预剪枝：数据分裂过程可能产生过拟合时就停止
    - 如果当前结点的样例数据小于某一个阈值就停止分裂：忽视了不纯度或错误，基于小样本空间的决策大概率是不可靠的
- 后剪枝 $1$：错误率降低剪枝
    - 先正常生成决策树，产生过拟合之后就回退
    - 基于统计分析，有多大的置信度可以将该分支剪掉
    - 从训练数据集中切分出一个集合作为验证集，验证剪枝之后的结果是否更好
- 后剪枝 $2$：规则后剪枝
    - 将决策树拆分为等价规则集合
    - 通过删除任何可能提高其估计准确性的先决条件来修剪每条规则
    - 将规则按所需顺序排序（按其估计精度）
    - 在对实例进行分类时，按照相同的顺序使用最终规则
    - 需要注意的是，这种剪枝方法有可能使得结果无法恢复为决策树
- 最小描述长度 $MDL$：最小化 $size(tree) + size(错误分类(tree))$

## 5. 决策树的改进

- 连续数据的处理：区间化

    - 取算术平均值
    - 取期望平均值

- 多个取值的属性：使用 $\tt GainRatio$ 替代

    $$GainRaito(S,A) = \frac{Gain(S,A)}{SplitInformation(S,A)}$$

    $$SplitInformation(S,A) = -\sum_{i=1}^{c} \frac{|S_i|}{|S|} \log_2 \frac{|S_i|}{|S|} $$

- 未知属性取值：用最大似然估计进行分类

- 有代价的属性：

    - $\frac{Gain^2(S,A)}{Cost(A)}$
    - $\frac{2^{Gain(S,A)} - 1}{(Cost(A)+1)^w}$，$w$ 取值为 $0$ 或 $1$，表示代价的重要性

## 6. 归纳学习假设

任一假设若在足够大的训练样例集中很好地逼近目标函数，它也能在未见实例中很好地逼近目标函数。

归纳学习算法可以在最大程度上保证输出假设在训练数据上符合目标概念。