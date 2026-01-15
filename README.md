# ☕ 咖啡因代谢与脑力状态计算器 (精简版)

## 1. 项目概述

本 Web 工具结合睡眠稳态模型 (Process S) 与睡眠预算倒推算法，旨在科学规划咖啡因摄入，在维持脑力高效的同时确保睡眠质量。

---

## 2. 核心科学模型

系统采用双层评估模型：

### 2.1 物理残留 (PK)

基于一级消除动力学计算血液咖啡因含量，作为睡眠红线判据。

$$C_t = C_0 \times (0.5)^{\frac{t}{t_{1/2}}}$$

（$t_{1/2}$：个体代谢半衰期）

### 2.2 大脑疲劳 (Process S)

利用 Borbély 双过程模型模拟清醒期间的腺苷堆积（困倦源）。

$$S(t) = 1 - e^{-\frac{t}{18.2}}$$

（18.2h 为成人压力增长常数）

### 2.3 有效感知 (Effective Perception)

修正疲劳后的实际提神强度，用于判断补给时机。

$$E_{level} = C_{physical} \times (1 - S_t)$$

---

## 3. 智能规划算法

### 3.1 睡眠预算 (Sleep Budgeting)

规划前先确立安全边界：

$$Budget = 50mg - \text{ResidualAtSleep}$$

### 3.2 补给策略 (回溯与维持)

当感知浓度低于设定值时：

- **标准单位优先**: 优先尝试在当前时刻添加 1份标准饮品。若未突破预算则执行。

- **分级回填 (Tiered Backfill)**: 若新增会导致失眠，则回溯寻找早期记录进行加浓。
  - **逻辑**: 早期摄入代谢更充分。
  - **路径**: 1.0倍 → 1.5倍 → 2.0倍 → 2.5倍 (封顶)。

---

## 4. 参考文献

- **Process S**: Borbély (1982); Achermann & Borbély (2003).
- **PK**: Fredholm et al. (1999); Nehlig (2018).
- **Adenosine**: Landolt (2008).

---

## 5. 预计更新 (Roadmap)

计划引入昼夜节律 (Process C) 构建三过程模型 (TPMA)：

$$\text{Alertness}(t) = \text{Baseline} + C(t) - S(t) + E_{caffeine}(t)$$

旨在精准预测午后低谷与睡眠禁区。

---

## 6. 技术栈

- **前端**: HTML5, JavaScript (ES6+), Tailwind CSS
- **可视化**: Chart.js
- **存储**: Browser LocalStorage