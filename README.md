# Game Dev Team

AI 游戏开发团队 —— 基于 [OpenCode](https://github.com/anomalyco/opencode) 的多 Agent 协作框架，用一句话启动从市场调研到完整实施文档的全流程游戏项目策划。

## 它能做什么

你对制作人（GameProducer）说一句话，比如：

> "我想做一款 Brain Puzzle 游戏"

团队会自动完成：

1. **需求采集** — 通过交互式提问引导你明确品类、市场、玩法、美术、变现等关键维度
2. **市场调研** — 调度调研专家分析品类机会、竞品格局、目标市场
3. **方向确认** — 呈现调研结论，请你做关键决策
4. **设计生产** — 并行调度游戏设计、美术指导、叙事文案、音频设计，产出完整方案
5. **文档汇编** — 汇总所有产出，交付可直接用于开发的《程序员实施文档》

## 团队架构

```
用户 ←→ GameProducer（制作人，唯一入口）
              │
              ├── GameResearcher（市场调研）
              ├── GameDesigner（游戏设计）
              ├── ArtDirector（美术指导 → 输出提示词 + 资产清单）
              ├── ArtAssetProducer（出图代理 → 按指南批量出图）
              ├── NarrativeDesigner（叙事文案）
              ├── AudioDesigner（音频设计）
              ├── LiveOps（发行运营）
              └── GameDataAnalyst（数据分析）
```

用户只能与 **GameProducer** 对话，其他专业 Agent 作为子代理由制作人统一调度。ArtAssetProducer 作为独立的出图代理，由用户在需要时手动调度。

### 角色职责

| 角色 | 职责 |
|------|------|
| 🎬 GameProducer | 编排中枢：需求采集、Agent 调度、进度管控、文档汇编 |
| 🔍 GameResearcher | 市场调研：品类分析、竞品调研、榜单解读、趋势追踪 |
| 🎮 GameDesigner | 游戏设计：核心循环、关卡设计、数值平衡、变现触点 |
| 🎨 ArtDirector | 美术指导：风格定义、AI 出图提示词输出、UI/UX 设计、角色设计、资产清单制定 |
| 🖼️ ArtAssetProducer | 美术生产：按风格指南批量生成全部游戏美术资产 |
| 📝 NarrativeDesigner | 叙事文案：世界观构建、角色塑造、对话脚本、UI 文案 |
| 🎵 AudioDesigner | 音频设计：BGM 设计、SFX 制作、动态音频系统 |
| 📢 LiveOps | 发行运营：ASO 优化、UA 买量、LiveOps 活动、社区运营 |
| 📊 GameDataAnalyst | 数据分析：留存分析、LTV 建模、AB 测试、变现漏斗 |

## 快速开始

### 前置要求

- 安装 [OpenCode](https://github.com/anomalyco/opencode)（或 [OhMyOpenAgent](https://github.com/code-yeongyu/oh-my-openagent)）
- 配置好 AI 模型的 API Key

### 使用方式

1. 将本项目克隆到本地（或直接复制 `opencode.json` + `prompts/` 目录到你的项目中）
2. 在项目根目录启动 OpenCode
3. 对 GameProducer 说出你的游戏想法，比如："我想做一款三消+装修的海外休闲手游"
4. 按照引导完成 5 个 Phase 的流程

### 项目结构

```
game-dev-team/
├── opencode.json          # Agent 配置（角色定义、权限、模型参数）
├── prompts/               # 各 Agent 的系统提示词
│   ├── game-producer.md   # 制作人（主编排器）
│   ├── game-researcher.md # 市场调研专家
│   ├── game-designer.md   # 游戏策划专家
│   ├── art-director.md    # 美术指导（风格定义 + 提示词输出，不出图）
│   ├── art-asset-producer.md # 美术资产批量生产者
│   ├── narrative-designer.md # 叙事文案专家
│   ├── audio-designer.md  # 音频设计专家
│   ├── live-ops.md        # 发行运营专家
│   └── game-data-analyst.md # 数据分析师
├── .sisyphus/             # 运行时工作目录（自动生成）
│   └── artifacts/         # 各阶段产出文档
└── LICENSE
```

## 工作流程

项目遵循 5 Phase 顺序执行，不可跳步：

```
Phase 1          Phase 2           Phase 3          Phase 4            Phase 5
需求采集    →    市场调研     →    用户确认    →    设计与生产    →    文档汇编
(交互式提问)      (调度 Researcher)  (呈现结论+决策)    (并行调度 4 个 Agent)   (汇编实施文档)
     ↓                ↓                 ↓                 ↓                 ↓
  需求摘要         调研报告          方向确认书      GDD+美术+叙事+音频    程序员实施文档
```

### Phase 1：需求采集

制作人通过 `question` 工具逐项引导，问题和选项根据你的回答动态调整。比如你说了"Brain Puzzle"，后续的玩法选项会自动给出画线解谜、物理机关、找茬观察等 Puzzle 细分方向，而不是泛泛的"有想法/没想好"。

互不依赖的问题可以一次批量问，有依赖关系的会等前置回答后再问。

### Phase 5：最终交付

产出的《程序员实施文档》包含 10 个章节，覆盖从产品概述到素材索引的完整内容，程序员拿到后可以直接开始实施。

## 自定义

### 修改 Agent 行为

编辑 `prompts/` 目录下对应的 `.md` 文件即可调整各 Agent 的行为。比如：
- 调整 GameProducer 的提问维度 → 编辑 `prompts/game-producer.md` 中的 Phase 1
- 调整 GameDesigner 的设计偏好 → 编辑 `prompts/game-designer.md`

### 调整权限和模型

编辑 `opencode.json` 中的 Agent 配置：
- `temperature`：控制创造性（数值越高越有创意，越低越严谨）
- `permission`：控制工具访问权限
- `model`：指定每个 Agent 使用的 AI 模型

### 扩展团队

在 `opencode.json` 的 `agent` 中添加新角色，并在 `prompts/` 中创建对应的提示词文件，然后在 GameProducer 的 `task` 权限中放行即可。

## License

[MIT](LICENSE) © 2026 青衫
