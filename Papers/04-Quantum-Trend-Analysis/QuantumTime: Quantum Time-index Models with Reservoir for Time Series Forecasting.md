# QuantumTime: Quantum Time-index Models with Reservoir for Time Series Forecasting

## 1. Paper Information（论文信息）

- **Title:** QuantumTime: Quantum Time-index Models with Reservoir for Time Series Forecasting
- **Conference:** ACM SIGKDD 2025
- **Code:** https://github.com/TJU-QUANTUM-LAB/QuantumTime
- **Research Direction:** Quantum Machine Learning, Time Series Forecasting, Efficient Learning
- **Keywords:** QINR, VQC, ESN, Reservoir Computing, Time-index Model
- **Classical Baseline:** DeepTIMe (ICML 2023)

---

## 2. Research Background（研究背景）

时间序列预测旨在利用历史观测数据预测未来的数据变化，广泛应用于：

- 电力负荷预测
- 金融趋势分析
- 交通流量预测
- 天气预测
- 工业设备状态监测
- 工业生产过程预测

传统时间序列预测方法包括 RNN、LSTM、Transformer、MLP 和 Deep Time-index Models (DeepTIMe)。

DeepTIMe 使用隐式神经表示（Implicit Neural Representation, INR），学习时间坐标与观测数据之间的映射关系。

然而，传统时间索引模型仍然存在以下问题：

1. 对复杂高频时间变化的表达能力存在局限。
2. 学习复杂时间特征可能需要大量可训练参数。
3. 时间坐标表示缺少显式的动态状态更新机制。
4. 对未来时间序列的外推能力仍有提升空间。

本文提出 QuantumTime，将量子隐式神经表示（QINR）与经典储备池计算（Reservoir Computing）结合，尝试在保持预测性能的同时减少模型的可训练参数。

---

## 3. Research Objectives（研究目标）

本文主要研究以下问题：

1. 如何利用量子变分电路提高复杂时间特征的表达能力？
2. 如何利用储备池计算增强时间序列的动态建模能力？
3. 如何减少时间序列预测模型的可训练参数？
4. 量子经典混合模型能否在长期时间序列预测任务中取得具有竞争力的结果？

核心研究目标：

> 利用小规模量子电路与经典储备池计算，在降低模型参数量的同时，实现有效的长期时间序列预测。

---

## 4. Proposed Method（核心方法）

QuantumTime 建立在 DeepTIMe 框架基础上，主要包含三个模块：

- Quantum Implicit Neural Representation (QINR)
- Echo State Network (ESN)
- Adaptive Ridge Regression

三个模块分别承担不同功能：

| Module | Function |
| --- | --- |
| QINR | 学习复杂时间特征 |
| ESN | 建模时间特征的动态变化 |
| Ridge Regression | 根据历史观测值计算预测权重 |

整体思想：

```text
QuantumTime = QINR + ESN + Ridge Regression
```

### 4.1 Deep Time-index Model（时间索引模型）

传统时间序列预测通常直接学习历史数据与未来数据之间的映射关系。

```text
Historical Data -> Neural Network -> Future Predictions
```

时间索引模型则通过时间坐标生成隐式时间特征，再根据历史观测数据拟合预测函数。

```text
z = f(t)

y_pred = W * z + b
```

其中：

- t：时间坐标。
- f：时间表示模型。
- z：时间特征表示。
- W：预测权重。
- b：偏置。
- y_pred：预测值。

例如，传统模型根据过去一段时间的电力消耗直接预测未来电力消耗。

时间索引模型则学习不同时间坐标对应的特征，并利用历史观测值建立时间特征与电力消耗之间的映射关系。

QuantumTime 延续这一思想，但使用 QINR 替代传统 INR，并引入 ESN 增强动态建模能力。

### 4.2 Quantum Implicit Neural Representation（量子隐式神经表示）

QINR 是本文的核心量子模块。

作者将变分量子电路（Variational Quantum Circuit, VQC）引入隐式神经表示，用于学习复杂的时间特征。

每个 QINRLayer 包含两个并行分支：

- Quantum Branch（量子分支）
- Classical Branch（经典分支）

#### Quantum Branch（量子分支）

量子分支主要包含以下操作：

1. 经典线性特征映射。
2. Batch Normalization。
3. 量子数据编码。
4. 参数化量子旋转门。
5. CNOT 纠缠操作。
6. 多组量子测量。

使用的主要量子门如下：

| Quantum Gate | Function |
| --- | --- |
| RX | 绕 X 轴旋转 |
| RY | 绕 Y 轴旋转 |
| RZ | 绕 Z 轴旋转 |
| CNOT | 建立量子比特之间的关联和纠缠 |
| Hadamard | 改变量子测量基 |
| SX | 参与测量前的量子态变换 |

量子电路通过旋转门编码经典数据，通过参数化量子门和纠缠操作进行特征变换。

公开代码通过 Pauli-Z 测量以及不同的测量前变换，获得四组量子测量结果，并将其拼接为经典特征向量。

由于量子旋转门具有三角函数形式，参数化量子电路能够构建具有频率特征的非线性表示。

作者希望利用这一特性提高模型对复杂高频时间变化的表达能力。

但是，量子电路是否比同等资源条件下的经典模型具有更好的表达能力，仍然需要通过实验验证。

#### Classical Branch（经典分支）

经典分支使用线性层和 ReLU 激活函数提取时间特征。

```text
z_classical = ReLU(W_classical * x + b_classical)
```

其中：

- x：输入特征。
- W_classical：经典线性层权重。
- b_classical：经典线性层偏置。
- z_classical：经典分支输出。

#### Feature Fusion（特征融合）

将量子分支与经典分支的输出进行拼接，再通过线性层融合。

```text
z_combined = Concatenate(z_quantum, z_classical)

z_output = Linear(z_combined)
```

其中：

- z_quantum：量子分支输出。
- z_classical：经典分支输出。
- z_output：融合后的时间特征。

因此，QINR 并不是完全由量子电路构成，而是一种量子经典混合神经网络。

### 4.3 QINR Architecture（QINR 架构）

```text
                 Temporal Input
                       |
                Linear Mapping
                       |
          +------------+------------+
          |                         |
    Quantum Branch           Classical Branch
          |                         |
    Linear Mapping             Linear Layer
          |                         |
    Batch Normalization           ReLU
          |
    Quantum Circuit
          |
    Quantum Measurements
          |                         |
          +------------+------------+
                       |
              Feature Concatenation
                       |
                Linear Fusion
                       |
              Temporal Representation
```

QINR 的主要特点是同时保留量子特征和经典特征，而不是完全使用量子电路替代经典神经网络。

### 4.4 Echo State Network（回声状态网络）

QINR 主要负责时间特征表示。

但是，仅依靠时间坐标映射，可能无法充分捕获时间序列的动态变化过程。

因此，作者引入 Echo State Network (ESN)。

ESN 是储备池计算（Reservoir Computing）的一种经典实现，主要包含：

- Input Layer
- Reservoir
- Readout Layer

与传统 RNN 不同，ESN 的储备池内部权重随机初始化后保持固定，不需要通过反向传播更新。

公开代码中的储备池状态更新公式为：

```text
h_current = (1 - alpha) * h_previous
            + alpha * sin(h_previous * W_res + z * W_in)
```

其中：

- h_current：当前储备池状态。
- h_previous：上一时刻的储备池状态。
- z：QINR 生成的时间特征。
- W_res：固定的储备池内部权重矩阵。
- W_in：固定的输入权重矩阵。
- alpha：Leaking Rate，用于控制状态更新比例。
- sin：非线性激活函数。

通过状态更新，储备池能够在一定范围内保留之前的时间特征信息。

公开代码采用滑动窗口和重叠窗口计算储备池状态，以减少逐时间点循环带来的计算开销。

需要注意：

1. 本文使用的是经典 ESN，而不是 Quantum Reservoir Computing。
2. 储备池内部权重固定，但 QINR 仍然需要梯度训练。
3. 公开实现中的储备池状态在不同窗口内独立初始化。
4. 历史和未来时间表示分别进行储备池计算，并非直接将历史最终状态传递至未来。

### 4.5 Adaptive Ridge Regression（自适应岭回归）

QuantumTime 使用 Ridge Regression 根据历史储备池状态和历史真实观测值计算预测权重。

优化目标可以简化表示为：

```text
Loss = Squared Prediction Error + Regularization Term
```

具体表示为：

```text
Loss = ||H * W - X||^2 + lambda * ||W||^2
```

其中：

- H：历史储备池状态矩阵。
- X：历史真实观测数据。
- W：预测权重矩阵。
- lambda：正则化系数。

省略偏置项时，岭回归的闭式解为：

```text
W = inverse(transpose(H) * H + lambda * I)
    * transpose(H) * X
```

其中：

- transpose(H)：矩阵 H 的转置。
- inverse()：矩阵求逆。
- I：单位矩阵。

实际代码通过线性方程求解获得权重，而不是直接计算逆矩阵。

获得预测权重后，利用未来储备池状态计算预测结果：

```text
Y_pred = H_future * W + b
```

其中：

- H_future：未来储备池状态。
- W：根据历史数据计算的预测权重。
- b：偏置。
- Y_pred：未来时间序列预测结果。

该方法不需要针对每个预测窗口单独进行大量梯度优化，而是通过矩阵求解获得自适应预测权重。

### 4.6 Overall Architecture（整体模型架构）

```text
Historical and Future Time Coordinates
                  |
                 QINR
                  |
        Temporal Representations
                  |
       +----------+----------+
       |                     |
Historical Features     Future Features
       |                     |
      ESN                   ESN
       |                     |
Historical States       Future States
       |                     |
       |                     |
Historical Observations      |
       |                     |
Ridge Regression             |
       |                     |
Adaptive Weights             |
       |                     |
       +----------+----------+
                  |
           Linear Forecasting
                  |
        Future Time Series Values
```

整体预测过程：

1. 输入历史观测数据及历史和未来时间坐标。
2. 使用 QINR 生成时间特征表示。
3. 将历史时间特征输入 ESN，生成历史储备池状态。
4. 利用历史储备池状态和历史真实观测值进行岭回归。
5. 计算自适应预测权重和偏置。
6. 将未来时间特征输入 ESN，生成未来储备池状态。
7. 使用预测权重计算未来时间序列。

未来真实观测值仅用于训练损失计算和预测性能评价，不作为预测阶段的模型输入。

---

## 5. Input and Output（输入与输出）

| Item | Description |
| --- | --- |
| Input X | 历史时间序列观测值 |
| Input X_time | 历史时间特征 |
| Input Y_time | 未来时间特征 |
| Quantum Module | QINR |
| Classical Module | ESN |
| Forecasting Head | Ridge Regression |
| Output | 未来时间序列预测值 |
| Learning Method | Supervised Learning |
| Task Type | Regression |
| Evaluation Metrics | MSE, MAE |

例如，在电力负荷预测任务中：

```text
Input:

Historical Electricity Consumption:
[120, 125, 130, 128, 135, ...]

Historical and Future Time Coordinates

Output:

Predicted Future Electricity Consumption:
[140, 145, 150, 148, ...]
```

模型输出的是连续数值，而不是分类标签。

本文本质上属于监督学习中的时间序列回归预测任务。

---

## 6. Experiments（实验设计与结果）

### 6.1 Experimental Objectives（实验目标）

论文主要验证以下问题：

1. QuantumTime 能否有效建模复杂时间序列？
2. QINR 能否减少时间表示模型的可训练参数？
3. ESN 能否增强时间序列外推能力？
4. QuantumTime 能否在真实时间序列预测任务中取得具有竞争力的结果？

### 6.2 Datasets（实验数据集）

论文涉及混沌时间序列和真实世界时间序列预测任务。

公开代码支持以下数据类型：

| Dataset | Description |
| --- | --- |
| ECL | 电力消耗时间序列 |
| ETTh | 小时级电力变压器温度数据 |
| ETTm | 分钟级电力变压器温度数据 |
| Custom CSV | 自定义时间序列数据 |

公开仓库提供了 ECL 数据集的四种预测长度配置。

ETT 数据集具有数据加载和划分支持，但不能仅根据代码支持情况认定所有 ETT 实验均已完整公开。

### 6.3 Experimental Settings（实验设置）

以下参数来自公开仓库的 ECL 实验配置和模型代码。

| Parameter | Setting |
| --- | --- |
| Deep Learning Framework | PyTorch |
| Quantum Framework | TorchQuantum |
| QINR Layers | 5 |
| QINR Hidden Dimension | 32 |
| Qubits per QINR Circuit | 8 |
| Quantum Circuit Blocks | 2 |
| Reservoir Size | 256 |
| Spectral Radius | 0.9 |
| Leaking Rate | 0.3 |
| Input Scaling | 0.5 |
| Batch Size | 256 |
| Optimizer | Adam |
| Learning Rate | 0.01 |
| Maximum Epochs | 100 |
| Early Stopping Patience | 15 |
| Loss Function | MSE |
| Dataset Split | 70% / 10% / 20% for ECL |

### 6.4 Forecasting Horizons（预测长度）

| Forecast Horizon | Historical Lookback | Total Sequence Length |
| --- | --- | --- |
| 96 | 864 | 960 |
| 192 | 960 | 1152 |
| 336 | 1008 | 1344 |
| 720 | 720 | 1440 |

不同预测长度使用不同的历史输入窗口。

因此，在与其他时间序列预测模型进行比较时，需要确保输入长度、预测长度和数据划分保持一致。

### 6.5 Evaluation Metrics（评价指标）

#### Mean Squared Error (MSE)

```text
MSE = sum((y_true - y_pred)^2) / N
```

MSE 用于衡量预测值与真实值之间的平均平方误差，对较大的预测误差更加敏感。

#### Mean Absolute Error (MAE)

```text
MAE = sum(abs(y_true - y_pred)) / N
```

MAE 用于衡量预测值与真实值之间的平均绝对误差。

其中：

- y_true：真实值。
- y_pred：预测值。
- N：评价样本中的数值总数。

MSE 和 MAE 越小，表示预测性能越好。

公开实现默认在标准化后的数据上计算评价指标。

### 6.6 Comparison with DeepTIMe（与经典基线对比）

| Comparison | DeepTIMe | QuantumTime |
| --- | --- | --- |
| Temporal Representation | Classical INR | Quantum-Classical QINR |
| Feature Extraction | Fourier Features + MLP | VQC + Classical Branch |
| Reservoir Computing | No | Classical ESN |
| Forecasting Head | Ridge Regression | ESN + Ridge Regression |
| Hidden Dimension | 256 | 32 |
| Quantum Circuits | No | Yes |
| Main Objective | Time-index Forecasting | Efficient Time-index Forecasting |

QuantumTime 在 DeepTIMe 基础上同时修改了时间表示模块和动态建模模块。

因此，两种模型的整体性能差异不能直接等同于量子模块的独立贡献。

### 6.7 Main Experimental Findings（主要实验结论）

根据此前整理的论文摘要信息，QuantumTime 在保持具有竞争力的预测性能的同时，相比 DeepTIMe 减少了至少 95% 的可训练参数。

主要研究结论：

- 量子经典混合时间表示具有一定的参数效率。
- 储备池计算能够为时间表示引入动态状态信息。
- QuantumTime 为轻量化时间序列预测提供了一种新的模型架构。

需要注意：

- 参数量减少不代表训练时间减少相同比例。
- 参数量减少不代表实际计算成本减少相同比例。
- 具有竞争力的预测性能不等于全面超过所有经典模型。
- 参数效率不能直接证明量子计算优势。

当前笔记尚未核验论文完整实验结果表，因此暂不记录各数据集的具体 MSE、MAE 和预测性能提升比例。上述参数缩减比例也应在取得论文原文后进一步核对。

---

## 7. Main Contributions（主要创新点）

### 7.1 Quantum Time Representation

将变分量子电路引入时间索引模型，利用量子经典混合结构学习复杂的时间特征。

### 7.2 Reservoir-Augmented Forecasting

将经典储备池计算引入时间索引预测框架，通过非线性状态更新增强时间特征的动态表达能力。

### 7.3 Parameter-Efficient Learning

通过小规模量子电路、较低维度的隐藏层和固定权重储备池，减少模型的可训练参数。

### 7.4 Hybrid Quantum-Classical Architecture

将量子特征表示、经典神经网络、储备池计算和自适应岭回归结合，构建完整的时间序列预测模型。

本文的主要贡献属于量子机器学习架构设计和高效时间序列预测，而不是提出新的量子计算硬件或量子纠错方法。

---

## 8. Limitations（局限性）

以下内容为基于公开代码和已有论文信息进行的分析，并非全部属于作者明确提出的局限性。

### 8.1 No Clear Quantum Computational Advantage

公开代码使用 TorchQuantum 进行量子电路模拟。

虽然模型减少了可训练参数，但尚不能据此证明其在真实量子硬件上的训练速度、推理速度或计算成本优于经典模型。

### 8.2 Quantum Contribution Requires Further Investigation

QuantumTime 同时引入 QINR 和 ESN。

为了区分两个模块的独立贡献，建议进一步开展以下消融实验：

| Model | Purpose |
| --- | --- |
| Classical INR + Ridge | 原始 DeepTIMe 基线 |
| QINR + Ridge | 验证量子表示模块的贡献 |
| Classical INR + ESN + Ridge | 验证经典储备池的贡献 |
| QINR + ESN + Ridge | 验证完整 QuantumTime 模型 |
| Parameter-matched Classical Model | 验证相同参数预算下的量子模型性能 |

需要判断预测性能究竟来自量子电路、经典储备池，还是两者的组合。

### 8.3 Parameter Efficiency vs. Computational Efficiency

可训练参数量减少并不代表整体计算成本降低。

模型仍然需要执行：

- Quantum Circuit Simulation
- Quantum Feature Measurement
- Reservoir State Computation
- Matrix Solving
- Classical Gradient Optimization

因此，应进一步比较：

- Training Time
- Inference Latency
- GPU Memory Consumption
- Total Parameter Count
- Quantum Circuit Depth
- Number of Quantum Measurements

只有综合考虑预测性能和计算资源，才能更加全面地评价模型的实际效率。

### 8.4 Limited Quantum Circuit Scalability

量子电路规模增加可能导致经典模拟成本快速增长。

对于 n 个量子比特，完整状态向量包含：

```text
Number of Quantum Amplitudes = 2^n
```

例如：

| Number of Qubits | State Vector Size |
| --- | --- |
| 4 | 16 |
| 8 | 256 |
| 12 | 4096 |
| 16 | 65536 |
| 20 | 1048576 |

因此，增加量子比特数量可能提高模型表达能力，但也可能显著增加经典模拟成本。

### 8.5 Limited Reservoir Memory

公开代码中的 ESN 使用局部滑动窗口进行状态计算。

每个窗口独立初始化储备池状态，历史和未来时间表示也分别进行储备池计算。

因此，模型没有直接将完整历史序列的最终储备池状态传递至未来预测阶段。

这种设计能够减少计算开销，但可能限制储备池对长距离时间依赖的建模能力。

### 8.6 Limited Noise Robustness Evidence

公开实现主要基于理想量子电路模拟。

仍需要进一步研究模型在以下噪声环境中的表现：

- Depolarizing Noise
- Readout Noise
- Gate Errors
- Spatially Heterogeneous Noise
- Time-varying Noise

真实量子设备中的噪声和有限测量次数可能影响时间特征表示的准确性。

### 8.7 Generalization under Distribution Shift

时间序列数据可能随着时间发生分布变化。

例如：

- 电力消耗模式变化。
- 极端天气事件。
- 交通流量异常。
- 工业设备性能退化。

模型在异常事件、跨数据集预测及非平稳时间序列环境下的泛化能力值得进一步验证。

### 8.8 Experimental Protocol

公开训练代码在每个 epoch 中同时计算训练集、验证集和测试集损失。

虽然模型检查点主要依赖验证集进行选择，但更加严格的实验流程应避免在训练期间反复查看测试集结果。

此外，公开代码会跳过 batch size 为 1 的验证或测试批次，需要在复现时检查是否影响最终评价样本数量。

---

## 9. Future Research Directions（未来研究方向）

以下内容为基于本文提出的潜在研究方向，不属于原论文已经完成的工作。

### 9.1 Lightweight Quantum Time Series Forecasting

研究更加轻量化的量子时间序列预测模型。

主要优化对象包括：

- Number of Qubits
- Number of Quantum Gates
- Quantum Circuit Depth
- Number of QINR Layers
- Reservoir Size
- Trainable Parameters

研究目标是在有限量子计算资源条件下保持较好的预测性能。

### 9.2 Quantum Architecture Search

将量子架构搜索方法引入 QuantumTime。

可以使用强化学习、进化计算或其他搜索算法自动优化：

- Quantum Gate Types
- Quantum Circuit Depth
- Qubit Connectivity
- Quantum Data Encoding Strategy
- Measurement Strategy
- Quantum-Classical Feature Fusion

例如，可以结合 TensorRL-QAS 的架构搜索思想，寻找更加适合时间序列预测任务的量子电路。

Reference:

https://github.com/Aqasch/TensorRL-QAS

### 9.3 Multi-Objective Quantum Learning

将预测性能和计算资源共同作为优化目标。

| Objective | Optimization Direction |
| --- | --- |
| MSE | Minimize |
| MAE | Minimize |
| Trainable Parameters | Minimize |
| Number of Qubits | Minimize |
| Quantum Gate Count | Minimize |
| Circuit Depth | Minimize |
| Training Time | Minimize |
| Inference Latency | Minimize |
| Noise Sensitivity | Minimize |

多目标优化问题可以表示为：

```text
Minimize:

Objective 1 = Prediction Error

Objective 2 = Trainable Parameters

Objective 3 = Quantum Circuit Depth

Objective 4 = Computational Cost

Objective 5 = Noise Sensitivity
```

通过 NSGA-II、强化学习或其他多目标优化算法寻找 Pareto 最优量子模型架构。

Reference:

https://github.com/anyoptimization/pymoo

### 9.4 Noise-Aware Quantum Forecasting

研究真实量子噪声对时间序列预测的影响。

主要研究内容：

1. 在量子电路中引入不同类型和强度的噪声。
2. 分析量子测量误差对时间特征表示的影响。
3. 研究噪声对长期预测误差的影响。
4. 根据量子硬件噪声动态调整电路结构。
5. 构建具有噪声鲁棒性的量子经典混合预测模型。

### 9.5 Quantum Reservoir Computing

原论文使用经典 ESN 作为储备池。

后续可以研究使用 Quantum Reservoir Computing (QRC) 替代经典储备池。

| Architecture | Temporal Representation | Reservoir |
| --- | --- | --- |
| DeepTIMe | Classical | None |
| QuantumTime | Quantum-Classical | Classical |
| Potential Extension 1 | Classical | Quantum |
| Potential Extension 2 | Quantum-Classical | Quantum |

通过对照实验研究量子储备池是否能够提供更好的动态表达能力、记忆能力和资源效率。

### 9.6 Industrial Time Series Forecasting

将 QuantumTime 扩展至工业时间序列预测任务，例如：

- Equipment Degradation Prediction
- Remaining Useful Life Prediction
- Industrial Energy Consumption Forecasting
- Production Process Monitoring
- Sensor Anomaly Prediction

进一步验证量子机器学习在实际工业数据中的应用价值。

---

## 10. Reproducibility（代码复现）

### 10.1 Open-source Resources

| Resource | Link |
| --- | --- |
| QuantumTime | https://github.com/TJU-QUANTUM-LAB/QuantumTime |
| DeepTIMe Paper | https://proceedings.mlr.press/v202/woo23b.html |
| Quantum Implicit Neural Representations | https://openreview.net/forum?id=50vc4HBuKU |
| TorchQuantum | https://github.com/mit-han-lab/torchquantum |
| PyTorch | https://github.com/pytorch/pytorch |

### 10.2 Project Structure

```text
QuantumTime/
|
|-- data/
|   |-- datasets.py
|
|-- experiments/
|   |-- base.py
|   |-- forecast.py
|   |-- configs/
|       |-- ECL/
|           |-- 96M.gin
|           |-- 192M.gin
|           |-- 336M.gin
|           |-- 720M.gin
|
|-- models/
|   |-- QuantumTIMe.py
|   |-- DeepTIMe.py
|   |-- modules/
|       |-- qinr.py
|       |-- inr.py
|       |-- regressors.py
|       |-- feature_transforms.py
|
|-- storage/
|   |-- datasets/
|   |-- experiments/
|
|-- utils/
|-- requirements.txt
|-- README.md
```

### 10.3 Key Source Files

| File | Function |
| --- | --- |
| models/QuantumTIMe.py | QuantumTime 整体模型 |
| models/DeepTIMe.py | 经典基线模型 |
| models/modules/qinr.py | 量子经典混合时间表示 |
| models/modules/inr.py | 经典隐式神经表示 |
| models/modules/regressors.py | ESN 和 Ridge Regression |
| experiments/forecast.py | 模型训练和测试 |
| data/datasets.py | 数据加载和预处理 |
| utils/metrics.py | 评价指标 |
| experiments/configs/ECL/ | 实验参数配置 |

### 10.4 Environment Requirements

| Package | Version |
| --- | --- |
| Python | 3.9 or above |
| PyTorch | 2.1.0 to below 2.3.0 |
| TorchQuantum | 0.1.8 |
| NumPy | 1.24.0 to below 2.0.0 |
| Pandas | 2.0.0 to below 2.3.0 |
| Scikit-learn | 1.3.0 or above |
| Gin-config | 0.5.0 or above |

### 10.5 Installation

```bash
git clone https://github.com/TJU-QUANTUM-LAB/QuantumTime.git

cd QuantumTime

conda create -n quantumtime python=3.10 -y

conda activate quantumtime

pip install -r requirements.txt
```

### 10.6 Dataset Preparation

将 ECL 数据集放置于：

```text
storage/datasets/electricity/electricity.csv
```

CSV 文件需要包含 date 时间列、数值特征列，以及配置文件指定的目标列。

### 10.7 Running Experiments

运行预测长度为 96 的实验：

```bash
python -m experiments.forecast --config_path=experiments/configs/ECL/96M.gin run
```

运行预测长度为 192 的实验：

```bash
python -m experiments.forecast --config_path=experiments/configs/ECL/192M.gin run
```

运行预测长度为 336 的实验：

```bash
python -m experiments.forecast --config_path=experiments/configs/ECL/336M.gin run
```

运行预测长度为 720 的实验：

```bash
python -m experiments.forecast --config_path=experiments/configs/ECL/720M.gin run
```

### 10.8 Recommended Reproduction Steps

- [ ] 创建独立 Python 环境。
- [ ] 安装 PyTorch 和 TorchQuantum。
- [ ] 下载并准备 ECL 数据集。
- [ ] 使用较小 batch size 完成 Smoke Test。
- [ ] 验证 QINR 前向传播。
- [ ] 验证 QINR 反向传播。
- [ ] 复现经典 DeepTIMe 基线。
- [ ] 复现 QuantumTime 主模型。
- [ ] 比较 MSE 和 MAE。
- [ ] 比较可训练参数量。
- [ ] 开展 QINR 和 ESN 消融实验。
- [ ] 比较训练时间、推理时间和显存占用。
- [ ] 开展量子噪声鲁棒性实验。

### 10.9 Reproduction Status

Status: Not Reproduced

目前已完成论文方法梳理和公开源代码分析，尚未实际运行完整复现实验。

---

## 11. Research Relevance（研究方向关联）

| Research Direction | Relevance |
| --- | --- |
| Time Series Forecasting | High |
| Trend Analysis | High |
| Quantum Machine Learning | High |
| Quantum Neural Networks | High |
| Efficient Quantum Learning | High |
| Reservoir Computing | High |
| Quantum Architecture Search | Potential Extension |
| Quantum Multi-Objective Learning | Potential Extension |
| Quantum Noise Estimation | Potential Extension |
| Quantum Error Correction | Low |
| Quantum Image Processing | Low |

本文主要属于趋势分析、时间序列预测、量子机器学习和高效学习方向。

量子架构搜索、多目标优化和噪声感知学习可以作为后续研究方向，但不属于原论文的核心研究内容。

---

## 12. Overall Evaluation（总体评价）

QuantumTime 是一种面向长期时间序列预测的量子经典混合机器学习模型。

该方法在 DeepTIMe 基础上引入量子隐式神经表示和经典储备池计算，分别用于增强时间特征表达能力和动态建模能力。

本文的主要研究价值包括：

1. 将量子变分电路应用于连续时间特征表示。
2. 结合经典储备池计算增强时间序列预测能力。
3. 在保持具有竞争力的预测性能的同时减少可训练参数。
4. 为轻量化量子机器学习提供新的架构设计思路。

但是，参数量减少并不能直接证明量子计算优势。

模型的实际计算效率、量子模块独立贡献、噪声鲁棒性和真实量子硬件性能仍需要进一步验证。

本文与普通量子神经网络回归任务的区别在于：

作者并不是简单地使用量子神经网络替代经典预测模型，而是针对时间序列预测中的特征表示和动态建模问题，分别设计了 QINR 和 ESN 两个模块。

本文最值得借鉴的研究思想：

> 利用小规模量子电路负责特征表示，利用经典储备池负责动态建模，通过量子与经典模块的功能互补实现高效学习。

后续可以结合量子架构搜索、多目标优化、噪声感知机制和工业时间序列预测任务，进一步探索具有实际应用价值的高效量子机器学习模型。

---

## 13. References（参考资源）

1. QuantumTime: Quantum Time-index Models with Reservoir for Time Series Forecasting, KDD 2025.

   https://github.com/TJU-QUANTUM-LAB/QuantumTime

2. Learning Deep Time-index Models for Time Series Forecasting, ICML 2023.

   https://proceedings.mlr.press/v202/woo23b.html

3. Quantum Implicit Neural Representations, ICML 2024.

   https://openreview.net/forum?id=50vc4HBuKU

4. TorchQuantum.

   https://github.com/mit-han-lab/torchquantum

5. TensorRL-QAS.

   https://github.com/Aqasch/TensorRL-QAS

6. pymoo: Multi-objective Optimization in Python.

   https://github.com/anyoptimization/pymoo

Note: TensorRL-QAS and pymoo are reference resources for potential future research rather than components of the original QuantumTime implementation.
