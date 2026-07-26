# 具身智能每周发展摘要 (Embodied Intelligence Weekly Digest)

> 聚焦全球具身智能与人形机器人产业，每周筛选 TOP 15 影响力事件，深度追踪硬件平台、VLA 模型、仿真数据、灵巧操作、产业化、政策监管六大维度。
>
> 方法论继承自 [GitHub Weekly Curation](https://github.com/zaitianzhiya/github-weekly-digest) 的工程实践。

## 方法论

采用"多源信息采集 + 五维影响力评价 + AI 深度分析"的人机协作模式：

1. **多源信息采集：** 覆盖全球核心企业官方发布、学术预印本、政策公告、科技媒体、行业数据库（共 30 个信息源，12 个生态分组）
2. **交叉验证去重：** 同一事件在多个独立来源确认后才纳入
3. **五维影响力加权：** 行业颠覆性(30%) + 技术突破度(25%) + 商业化进展(20%) + 生态影响力(15%) + 政策资本信号(10%)
4. **AI 深度分析：** 每个 TOP 15 事件按"事件概述 → 关键数据 → 影响分析 → 下一步关注"结构展开
5. **跨事件趋势洞察：** 识别多个事件指向的共同方向（如 VLA 模型范式转换、人形机器人量产拐点）

## 六维分类

| # | 分类 | 标签 | 说明 |
|---|------|------|------|
| 1 | 机器人硬件平台 | `#hardware` | 人形机器人/机械臂/灵巧手/关节/传感器发布 |
| 2 | VLA 模型与算法 | `#vla-model` | Vision-Language-Action、世界模型、端到端学习 |
| 3 | 仿真与数据 | `#simulation` | 仿真平台、Sim-to-Real、数据采集、遥操作 |
| 4 | 操作与感知 | `#manipulation` | 灵巧操作、抓取、导航、SLAM、触觉感知 |
| 5 | 产业化与商业 | `#industry` | 量产、交付、融资、IPO、供应链动态 |
| 6 | 政策与监管 | `#policy` | 政府政策、行业标准、安全监管、伦理规范 |

## 信息源体系

### Tier 1: 原始数据源（17 个）

| 类别 | 来源 | 采集方式 |
|------|------|---------|
| 全球头部企业 | Tesla Optimus / Figure AI / Boston Dynamics / Agility Robotics / 1X Technologies | Web Search |
| 中国头部企业 | 宇树科技 / 智元机器人 / 小鹏机器人 / 星动纪元 / 银河通用 | Web Search |
| 全球创业公司 | Skild AI / Physical Intelligence (π) | Web Search |
| 学术界 | arXiv cs.RO / arXiv cs.AI (embodied filter) | RSS |
| 开源社区 | GitHub 具身智能话题 | API |
| 中国政策 | 工信部 / 网信办 | Web Search |

### Tier 2: 引用数据源（13 个）

| 类别 | 来源 |
|------|------|
| 中国科技媒体 | 36氪 / 机器之心 / 量子位 / IT之家 / 界面新闻 |
| 英文科技媒体 | TechCrunch Robotics / The Verge AI / VentureBeat AI |
| 行业研究 | IDC / TrendForce / 中国信通院 |
| 资本市场 | 投中网 / 东方财富 |
| 开源策展 | Awesome-VLA / Datawhale 具身智能教程 |

## 五维影响力权重

| 维度 | 权重 | 说明 |
|------|------|------|
| **行业颠覆性** | 30% | 对具身智能产业格局的重塑程度 |
| **技术突破度** | 25% | 技术本身的新颖性和难度 |
| **商业化进展** | 20% | 量产/交付/融资/IPO/落地程度 |
| **生态影响力** | 15% | 对开发者/供应链/下游生态的波及面 |
| **政策资本信号** | 10% | 融资规模/政策力度/市场预期 |

## 项目结构

```
embodied-intelligence-weekly/
├── .github/workflows/
│   ├── weekly-digest.yml       # 每周一 18:37 CST 主工作流
│   └── watchdog.yml            # 周一 3 次补发检查
├── config/
│   ├── sources.yml             # 30 个信息源 + 12 个生态分组
│   ├── keywords.yml            # 正/负向关键词 + 重点关注组织
│   └── quality.yml             # 五维评分 + 置信度 + 分类体系
├── prompts/
│   ├── weekly-deep.md          # 深度分析 Prompt（禁止裸术语/两层阅读）
│   ├── taxonomy.md             # 分类 + 评分规则
│   └── feedback-rules.md       # 反馈闭环
├── output/
│   └── YYYY-WNN.md              # 周报输出
├── feedback/                    # 读者反馈（注入 AI Prompt）
├── README.md
└── CLAUDE.md
```

## 部署

- 📋 GitHub Actions 每周一 UTC 10:37（北京时间 18:37）自动运行
- 🛡️ 看门狗 3 次检查补发
- 📬 反馈: 提交到 `feedback/YYYY-WNN.md`
- 🔄 频率: 每周一发布

## 相关项目

- [GitHub Weekly Digest](https://github.com/zaitianzhiya/github-weekly-digest) — 方法论源头
- [领域知识自动化收集评价存储部署发布-完整方法论](../领域知识自动化收集评价存储部署发布-完整方法论.md) — 通用方法论指南
