# ch4 马尔可夫模型和隐马尔可夫模型

## 1. 马尔可夫模型

- 应用背景：天气预报、疾病传播预测、语音识别、中文输入法、人口预测、生物信息学

- 给定一个数据序列，数据存在先后关系 $D = \{X_1, X_2 \dots X_N\}$
    - 一阶马尔可夫假设：当前时刻 $n$ 的状态只与上一个时刻 $n-1$ 的状态相关，而与时刻 $n-2$ 及其之前时刻的状态无关
    - $P(X_n|X_{n-1}\dots X_2, X_1) \approx P(X_n | X_{n-1})$
    - $P(D|M)=P(X_1) \Pi_{n=2}^N P(X_n|X_{n-1})$
- 转移概率：$a_{i,j} = P(x_n = S_j | X_{n-1} = S_i)$
    - $a_{i,j} \ge 0$
    - 时间不变性：$P(x_n = S_j | X_{n-1} = S_i) = P(x_{n+T} = S_j | X_{n-1+T} = S_i)$
    - 可以生成转移概率矩阵，其中 $\sum_{j=1}^M a_{i,j} = 1,\ \forall i \in [1,M]$

## 2. 隐马尔可夫模型

![image-20241203151144950](C:/Users/doure/AppData/Roaming/Typora/typora-user-images/image-20241203151144950.png)

需要知道如下数据集：

- $S = \{s_1 \dots s_N\}$：隐状态取值
- $K = \{k_1 \dots k_M\}$：观测值
- $\Pi = \{\pi_i\}$：初始状态概率
- $A = \{a_{ij}\}$：转移概率
- $B = \{b_{ij}\}$：观测状态的概率（输出概率）$b_{i,j} = P(y_n = K_j | x_n = S_i)$

$P(u_1\dots u_n|w_1\dots w_n) = \Pi_{i=1}^n P(u_i|w_i)$

隐马尔可夫模型中，主要利用了**一阶马尔可夫假设**和**输出独立性假设**。

## 3. 评估问题

![image-20241203151820752](C:/Users/doure/AppData/Roaming/Typora/typora-user-images/image-20241203151820752.png)

![image-20241203151848651](C:/Users/doure/AppData/Roaming/Typora/typora-user-images/image-20241203151848651.png)

这是一种枚举算法，计算时间复杂度为 $O(2TN^T)$，其中 $T$ 表示所有可能状态序列的长度。

**前向算法**：一种动态规划算法

- 定义 $\alpha_t(i) = P(o_1 \dots o_t,\ x_t = i | \mu)$，于是 $P(O|\mu) = \sum_{i=1}^N \alpha_T(i)$
- 易得 $\alpha_{t+1}(j) = \sum_{i=1}^N \alpha_t(i)a_{ij}b_{jo_{t+1}}$
- 该方法计算时间复杂度为 $O(N^2T)$

**后向算法**：

![image-20241203153135045](C:/Users/doure/AppData/Roaming/Typora/typora-user-images/image-20241203153135045.png)

## 4. 解码问题

根据观察到的输出序列，求解隐藏序列，即求满足 $\arg\max_X P(X|O)$ 的 $X$。

**维特比算法**：

![image-20241203154127350](C:/Users/doure/AppData/Roaming/Typora/typora-user-images/image-20241203154127350.png)

![image-20241203154214289](C:/Users/doure/AppData/Roaming/Typora/typora-user-images/image-20241203154214289.png)

![image-20241203154347181](C:/Users/doure/AppData/Roaming/Typora/typora-user-images/image-20241203154347181.png)

## 5. 隐马尔可夫模型的应用

语音识别、中文输入法、词性标注、基因分析、疾病诊断等任何存在线性序列依赖的现象。