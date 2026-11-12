# AI + Quantum Computing Terminology

本文件用于统一整理人工智能与量子计算交叉研究中的常用专业术语，便于论文阅读、实验复现和学术交流。

## 1. Quantum Computing Fundamentals | 量子计算基础

**Quantum Computing（量子计算）**：利用量子力学规律处理信息的计算方式，通过量子态制备、量子门操作和测量执行计算任务。

**Qubit（Quantum Bit，量子比特）**：量子计算的基本信息单位，可以处于 |0⟩、|1⟩ 及两者的叠加态。

**QPU（Quantum Processing Unit，量子处理器）**：执行量子门操作、量子态演化与测量的计算硬件。

**Quantum State（量子态）**：描述量子系统状态的数学对象，可用于计算测量结果及其概率。

**Superposition（量子叠加）**：量子系统可以处于多个基态的线性组合，测量时按照相应概率得到具体结果。

**Entanglement（量子纠缠）**：多个量子系统之间存在无法简单分解为各子系统独立状态的量子关联。

**Quantum Gate（量子门）**：对量子比特执行操作的基本单元，例如 H 门、X 门和 CNOT 门。

**Quantum Circuit（量子电路）**：由量子门、测量等操作构成的计算过程，用于实现量子算法。

**Quantum Measurement（量子测量）**：从量子系统中获取经典测量信息的过程，通常得到 0、1 等结果。

**Shots（重复测量次数）**：对同一量子电路重复执行和测量的次数，用于统计测量结果的概率分布。

**Quantum Simulation（量子模拟）**：利用量子计算方法研究分子、材料或其他量子系统的状态及演化。

**Hamiltonian（哈密顿量）**：描述物理系统能量及其动力学性质的数学算符。

**VQE（Variational Quantum Eigensolver，变分量子本征求解器）**：利用参数化量子电路测量能量，并通过经典优化器调整参数，以估计量子系统的低能量状态。

## 2. Quantum Error Correction | 量子纠错与噪声估计

**QEC（Quantum Error Correction，量子纠错）**：通过量子编码、稳定子测量和错误解码等方法，保护逻辑量子信息，降低噪声造成的影响。

**Physical Qubit（物理量子比特）**：量子硬件中实际存在的量子比特，是实现量子门操作和测量的基本物理单元。

**Logical Qubit（逻辑量子比特）**：通过多个物理量子比特编码得到、受到量子纠错保护的逻辑信息单位。

**Surface Code（表面码）**：一种常见的拓扑量子纠错码，通过二维排列的物理量子比特和局部稳定子测量实现错误检测与纠正。

**Code Distance（码距）**：量子纠错码的重要参数，表示能够实现非平凡逻辑操作的最小物理错误算符权重，通常记为 d。

**Stabilizer（稳定子）**：用于定义量子纠错码空间的算符，通过测量稳定子可以获取与错误有关的信息。

**Syndrome（错误症状信息）**：由稳定子测量结果构成的校验信息，可用于判断量子系统可能发生的错误。

**Detection Event（检测事件）**：检测器测量结果与预期关系不一致时产生的事件，常用于构建量子纠错解码问题。

**DEM（Detector Error Model，检测器错误模型）**：描述不同错误机制发生的概率，以及它们可能触发的检测事件和逻辑可观测量变化的模型。

**Decoding Graph（解码图）**：根据错误模型构建的图结构，用节点和带权边表示检测事件之间可能的错误关联。

**MWPM（Minimum Weight Perfect Matching，最小权完美匹配）**：一种常用量子纠错解码方法，通过在加权图中寻找总权重最小的匹配，推断可能发生的错误。

**Decoder（解码器）**：根据 Syndrome 或检测事件等信息，推断错误修正信息的算法或系统。

**LER（Logical Error Rate，逻辑错误率）**：量子纠错后逻辑信息仍然发生错误的比例，用于衡量纠错性能。

**Depolarizing Noise（退极化噪声）**：一种常见的量子噪声模型，用随机 Pauli 错误描述量子信息受到的干扰。

**Non-stationary Noise（非平稳噪声）**：统计特性随时间或实验条件变化的噪声，例如噪声强度漂移或突变。

**Noise Estimation（噪声估计）**：利用测量数据或实验统计结果，估计量子系统中噪声的强度、分布或有效错误机制。

**Stim**：高性能稳定子电路模拟器，常用于量子纠错电路模拟和检测事件采样。

**PyMatching**：基于匹配算法的量子纠错解码工具，可用于 MWPM 解码和逻辑错误率评估。

## 3. Quantum Machine Learning | 量子机器学习

**QML（Quantum Machine Learning，量子机器学习）**：研究量子计算与机器学习相结合的算法和模型，包括量子分类、量子回归、量子核方法等。

**QNN（Quantum Neural Network，量子神经网络）**：通常利用可训练的参数化量子电路构建的机器学习模型，可用于分类、回归和量子数据分析。

**PQC（Parameterized Quantum Circuit，参数化量子电路）**：包含可调量子门参数的量子电路，常用于变分量子算法和 QNN。

**VQC（Variational Quantum Classifier，变分量子分类器）**：通过训练参数化量子电路，实现数据分类的量子机器学习模型。

**QSVM（Quantum Support Vector Machine，量子支持向量机）**：利用量子特征映射或量子核方法辅助支持向量机分类的模型。

**Quantum Kernel（量子核方法）**：利用量子态或量子电路计算数据之间的核函数，用于分类等机器学习任务。

**QCNN（Quantum Convolutional Neural Network，量子卷积神经网络）**：借鉴卷积神经网络分层结构设计的量子模型，可用于量子态分类等任务。

**QGAN（Quantum Generative Adversarial Network，量子生成对抗网络）**：将量子模型引入生成对抗学习，用于学习数据分布或生成量子态。

**Hybrid Quantum-Classical Learning（量子经典混合学习）**：结合量子电路计算和经典机器学习、参数优化方法的学习框架。

## 4. Optimization and Evolutionary Computation | 优化与进化计算

**Combinatorial Optimization（组合优化）**：在有限或离散的候选方案中寻找满足约束的较优解，例如路径规划和任务分配。

**QAOA（Quantum Approximate Optimization Algorithm，量子近似优化算法）**：利用参数化量子电路与经典优化器求解组合优化问题的算法。

**Evolutionary Computation（进化计算）**：借鉴自然进化机制，通过种群搜索、选择、交叉和变异等方式求解优化问题的方法。

**GA（Genetic Algorithm，遗传算法）**：一种典型进化优化算法，通过模拟选择、交叉和变异等操作搜索候选解。

**PSO（Particle Swarm Optimization，粒子群优化）**：受群体协同行为启发，通过粒子位置和速度更新寻找优化问题的较优解。

**QPSO（Quantum-behaved Particle Swarm Optimization，量子行为粒子群优化）**：利用量子行为启发的位置更新机制改进粒子群搜索的算法，通常仍运行在经典计算机上。

**Multi-objective Optimization（多目标优化）**：同时考虑多个可能存在冲突的优化目标，例如成本、效率和能耗。

**Pareto Optimality（帕累托最优）**：在多目标优化中，无法在不使其他目标变差的情况下继续改善某个目标的解所具有的性质。

**Reinforcement Learning（强化学习）**：智能体通过与环境交互，根据奖励信号学习决策策略的机器学习方法。

## 5. Intelligent Learning and Architecture Search | 高效学习与架构搜索

**NAS（Neural Architecture Search，神经网络架构搜索）**：利用搜索或优化算法自动寻找神经网络结构的方法。

**QNAS（Quantum Neural Architecture Search，量子神经网络架构搜索）**：自动搜索量子神经网络结构、量子门组合和电路配置的方法。

**Efficient Learning（高效学习）**：以较少的数据、计算资源或训练成本获得有效模型的学习方法及研究目标。

**Few-shot Learning（小样本学习）**：利用少量标注样本进行模型学习或快速适应新任务的方法。

**Transfer Learning（迁移学习）**：将已有任务中获得的知识迁移到新任务，以减少训练成本或数据需求。

**Trend Analysis（趋势分析）**：通过统计方法或机器学习分析数据随时间或条件变化的规律，并根据需要进行趋势预测。

## 6. Cryptography and Information Security | 密码与信息安全

**Quantum Cryptography（量子密码学）**：研究利用量子物理原理实现密码相关任务和安全通信的方法。

**QKD（Quantum Key Distribution，量子密钥分发）**：利用量子信息传输与经典通信协议实现密钥协商，并检测潜在窃听行为的技术。

**PQC（Post-Quantum Cryptography，后量子密码学）**：研究能够抵抗已知量子攻击的经典密码算法和协议。

**Shor's Algorithm（Shor 算法）**：一种量子算法，可在理想量子计算模型下高效求解整数分解和离散对数等问题，对部分传统公钥密码体系具有重要影响。

## 7. Image Processing and Remote Sensing | 图像与遥感处理

**Image Classification（图像分类）**：根据图像内容判断其所属类别的任务。

**Object Detection（目标检测）**：识别图像中目标的类别与位置的任务。

**Image Segmentation（图像分割）**：将图像划分为不同像素区域，用于区分目标或不同语义类别。

**Remote Sensing Image Processing（遥感图像处理）**：对卫星、航空等遥感平台获取的影像进行分类、检测、分割和分析。

**Change Detection（变化检测）**：比较不同时期获取的遥感影像，识别地表覆盖或目标发生变化的区域。

**Quantum Image Processing（量子图像处理）**：研究利用量子信息表示和量子计算方法执行图像编码、变换、分析等任务。

**Quantum-inspired Image Processing（量子启发式图像处理）**：借鉴量子计算或量子力学相关思想设计图像处理算法，不一定需要真实量子硬件。

---

## Terminology Maintenance | 术语维护说明

1. 每个专业术语采用统一的英文名称、缩写及中文解释。
2. 新术语根据研究方向补充到对应章节。
3. 对已经确认的定义保持统一，避免在不同论文笔记中出现不一致的解释。
4. 对容易混淆的术语，补充必要的适用范围或区别说明。
5. 同一缩写可能代表不同概念，例如 PQC 可指参数化量子电路，也可指后量子密码学，阅读时应根据上下文区分。
