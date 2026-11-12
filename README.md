# AI + Quantum Computing Research Notes

本项目用于持续整理人工智能与量子计算交叉领域的文献阅读、专业术语、算法研究及实验复现记录，重点关注量子计算与人工智能算法的结合方式、实际应用及研究进展。

This repository collects literature reviews, terminology, research notes, and reproducible experiments related to Artificial Intelligence and Quantum Computing.

## 1. Research Directions | 研究方向

### 1.1 AI-Assisted Quantum Computing | AI 辅助量子计算

- **AI-Assisted Quantum Error Correction and Noise Estimation（AI 辅助量子纠错与噪声估计）**：研究利用机器学习估计量子噪声、构建检测器错误模型（DEM）、优化解码算法和匹配权重，提高量子计算的可靠性。
- **Quantum Circuit Optimization（量子电路优化）**：研究利用强化学习、搜索算法等方法优化量子电路结构、量子门数量和电路深度。

### 1.2 Quantum Machine Learning and Intelligent Optimization | 量子机器学习与智能优化

- **Quantum Machine Learning（量子机器学习，QML）**：研究利用量子算法和量子电路完成分类、回归、数据分析和生成建模等任务。
- **Quantum Neural Networks（量子神经网络，QNN）**：研究参数化量子电路的模型设计、训练方法及其在分类、预测等任务中的应用。
- **Combinatorial Optimization and Logistics Scheduling（组合优化与物流调度）**：研究量子优化算法及量子启发式算法在路径规划、任务分配和资源调度等问题中的应用。
- **Evolutionary Computation（进化计算）**：研究进化算法与量子计算、量子启发式计算相结合的优化方法。
- **Quantum Multi-objective Learning and Optimization（量子多目标学习与优化）**：研究利用量子计算或量子启发式算法同时优化多个目标，例如成本、效率和资源利用率。

### 1.3 Intelligent Algorithms and Model Optimization | 智能算法与模型优化

- **Neural Architecture Search（神经网络架构搜索，NAS）**：研究利用搜索与优化算法自动设计神经网络结构，以及量子神经网络的电路架构搜索方法。
- **Efficient Learning（高效学习）**：关注小样本学习、模型轻量化、计算资源优化及高效训练等研究。
- **Trend Analysis（趋势分析）**：研究利用统计分析、机器学习和时间序列模型进行趋势预测与变化规律分析，并关注相关量子算法的探索。

### 1.4 Applications and Security | 行业应用与计算安全

- **Cryptography and Information Security（密码与信息安全）**：关注量子计算对密码体系的影响、量子密码分析，以及相关安全算法与技术。
- **Image Processing Optimization（图像处理优化）**：研究传统 AI、量子计算及量子启发式方法在图像识别、特征提取和图像处理优化中的应用。
- **Remote Sensing Image Processing（遥感图像处理）**：关注遥感图像分类、目标检测、变化检测及量子机器学习相关应用。

## 2. Repository Structure | 项目目录

| 目录 | 主要内容 |
|---|---|
| `Paper_List.md` | 论文汇总、研究方向、主要成果和阅读状态 |
| `Papers/` | 按研究方向分类整理论文精读笔记 |
| `Glossary/` | 专业术语及统一解释 |
| `Experiments/` | 算法复现、实验配置、结果和问题记录 |
| `Weekly-Notes/` | 每周学习进展、文献总结与研究思考 |

## 3. Current Research Focus | 当前研究重点

### AI-Assisted Quantum Error Correction

目前主要研究 AI 辅助量子纠错中的噪声估计与解码优化，包括：

- 非平稳噪声环境下的量子纠错性能分析。
- 基于 Syndrome 数据的检测器错误模型（DEM）估计。
- MWPM 解码权重校准与更新策略。
- 经典机器学习方法与传统量子纠错算法的性能比较。

### Extended Research Topics

在现有研究基础上，进一步关注量子机器学习、量子神经网络、组合优化、进化计算、网络架构搜索、高效学习及图像处理等方向，重点调研相关算法、开源项目、实验条件及可复现性。

## 4. Research Tools | 研究工具

- **Quantum Error Correction**：Stim、PyMatching
- **Machine Learning**：PyTorch
- **Quantum Computing**：Qiskit、PennyLane、TorchQuantum
- **Numerical Computing**：NumPy、SciPy、Pandas
- **Development**：Python、Jupyter Notebook、VS Code

## 5. Research Notes and Updates | 学习与更新

本仓库将持续更新：

1. AI 与量子计算交叉领域的代表性论文及研究进展。
2. 专业术语、基础理论与算法学习笔记。
3. 开源论文的复现过程、实验结果和方法对比。
4. 阶段性学习总结与后续研究计划。

**Note:** 本项目包含量子算法、经典 AI 算法以及量子启发式计算方法。相关论文将根据实际使用的算法和计算资源进行区分。
