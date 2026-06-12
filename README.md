# Concept Studio Spread

> 用 AI + Markdown 管理个人知识资产中的**学术概念沉淀**。

一套 AI Agent 工作流，帮你从阅读、对话、思考中提取概念，建成结构化的个人概念库。

框架无关——适用于任何支持自定义 Skill / Prompt / Agent 指令集的 AI 环境：
**Claude Code、Codex、Cursor、Windsurf、Continue.dev** 等。

---

## 一句话说明

这个仓库是**工具**——怎么建概念页、怎么管理概念库、怎么让概念之间产生联系。

如果你想要**现成的内容**（700+ 张写好的概念卡片），那是另一个项目：**[Noosphere](https://github.com/MERJIC/noosphere)**。下面会详细说两者的关系。

---

## 它能做什么

| 功能 | 一句话 |
|------|--------|
| **寓言故事** | AI 选一个冷门学术原理写成寓言，听完可存入概念库 |
| **摄入概念** | 丢一个 URL 或一段文字，AI 自动提取值得沉淀的概念并建页 |
| **概念跳跃** | 从已有概念出发，每次推荐 3 个新方向，链式探索 |
| **圆桌讨论** | 就任意议题发起多视角结构化辩论 |
| **关联分析** | 扫描全库链接关系，识别孤立节点和概念集群 |
| **知识卡片** | 将概念页转为图文卡片 |

产出物是 **标准化的 Markdown 概念页**，兼容 Obsidian（支持 `[[]]` 双向链接）。

---

## 谁适合用

- 用 Obsidian / VS Code 等 Markdown 编辑器管理笔记的人
- 有跨学科阅读习惯，想系统沉淀学术概念的人
- 使用任何 AI 编程助手的人（Claude Code、Codex、Cursor 等）
- 不想从零设计知识库结构，想要一套「拿来就能写」的工作流的人

## 不适合

- 需要协同编辑或云端同步方案的人（这是本地 Markdown 工作流）
- 想要全自动知识图谱可视化的人（关联分析是文本报告，不是图形界面）

---

## 安装（3 步）

### 第 1 步：下载

**方式 A — 克隆到你的项目目录下（推荐）**

在你的概念库项目根目录执行：

```bash
git clone https://github.com/MERJIC/concept-studio-spread.git skills/concept-studio-spread
```

装完后你的目录长这样：

```
my-concept-lib/
├── 概念页/                        # 你的概念 .md 文件
├── skills/
│   └── concept-studio-spread/     # ← 工具在这里
│       ├── SKILL.md
│       ├── modules/
│       └── scripts/
└── roundtable/                    # 圆桌记录（自动生成）
```

**方式 B — 下载 ZIP 解压**

1. 打开 [仓库主页](https://github.com/MERJIC/concept-studio-spread)
2. 点绿色的 **Code → Download ZIP**
3. 解压后把 `concept-studio-spread` 文件夹放到你项目的 `skills/` 目录下

不需要 Git。解压就能用。

### 第 2 步：配置路径

打开 `skills/concept-studio-spread/SKILL.md`，找到开头的 `config` 部分：

```yaml
config:
  concept_lib_root: "{ROOT}"
```

把 `{ROOT}` 替换为你的概念库根目录的**绝对路径**。例如：

```yaml
config:
  concept_lib_root: "/Users/yourname/Documents/my-concept-lib"
```

macOS 用户：在 Finder 里打开概念库文件夹，按 `Option + Command + C` 复制完整路径，粘贴进来就行。

Windows 用户：在文件资源管理器的地址栏复制路径。

**就改这一行。其他不用动。**

### 第 3 步：创建文件夹

你的概念库里需要有这些文件夹（没有的话手动创建）：

```
my-concept-lib/
├── 概念页/          # 概念 .md 文件放这里
└── roundtable/      # 圆桌讨论记录放这里（可选）
```

```bash
mkdir -p 概念页 roundtable
```

完成。现在可以开始用了。

---

## 怎么用

### 寓言故事

对 AI 说：

```
讲个寓言
```

或指定领域：

```
讲个寓言 经济学
```

AI 会选一个冷门原理，写成故事，讲完揭示原理名。听完觉得有价值，说「建页」就自动存入概念库。

### 摄入概念

丢 URL 或文字：

```
摄入 https://example.com/article-about-cognitive-bias
```

或直接粘贴：

```
摄入 [粘贴一段文字]
```

AI 会从中提取 1-5 个候选概念，去重后让你选。确认后自动建页。

### 概念跳跃

```
跳一跳
```

AI 从你的概念库里随机选一个起点，推荐 3 个新方向。选一个继续跳，或者「沉淀这个」存入库。

也可以指定起点：

```
跳一跳 从「证实偏差」出发
```

### 圆桌讨论

```
圆桌讨论 AI 是否具有创造力？
```

AI 自动选人、主持辩论、生成结构图。讨论记录自动保存到 `roundtable/` 目录。

### 关联分析

```
更新图谱
```

扫描全库链接关系，报告孤立节点、集群归属建议、断链记录。

### 知识卡片

```
知识卡片 证实偏差
```

将已有概念页转为图文卡片。

---

## 建出来的概念页长什么样

每个概念是一个 `.md` 文件，放在 `概念页/` 目录下：

```markdown
---
name: 证实偏差（Confirmation Bias）
domain: [心理学]
date: 2025-05-20
source: 寓言故事
tags: [discipline/认知心理学, apply/自我, apply/决策]
---

## 核心机制

人倾向于寻找、解释、记忆那些支持自己既有信念的信息...

## 入口场景

1973 年冬天，普林斯顿大学的会议室里...

## 现实锚点

- **信息茧房**：算法推荐强化既有观点...
- **投资决策**：只看利空/利好中符合预期的那部分...

## 适用边界

不等于「所有信念都是错的」...
```

完整格式规范见 `modules/page-spec.md`。

---

## 和 Noosphere 的关系

```
┌─────────────────────────┐     ┌──────────────────────────────┐
│      Noosphere          │     │   Concept Studio Spread       │
│                         │     │                              │
│  700+ 张概念卡片        │ ←── │  工具：建页 / 摄入 / 跳跃     │
│  (内容)                 │     │  工具：圆桌 / 分析 / 卡片     │
│                         │     │  (工具链)                     │
│  github.com/MERJIC/     │     │  github.com/MERJIC/           │
│  noosphere              │     │  concept-studio-spread        │
└─────────────────────────┘     └──────────────────────────────┘
        内容                               工具
    可以直接用                      装到项目里才能用
```

**三种用法：**

| 你想要什么 | 怎么做 |
|-----------|--------|
| 读概念，不建库 | 只用 Noosphere，直接翻 [INDEX.md](https://github.com/MERJIC/noosphere/blob/main/概念页/INDEX.md) |
| 在 700+ 概念基础上建自己的库 | Fork Noosphere + 装 Spread，往里加自己的概念 |
| 从零开始建概念库 | 只装 Spread，从零积累 |

Fork Noosphere 拿内容，装 Spread 拿工具。两者独立，各取所需。

---

## 可选：配置脚本

skill 附带两个 Python 脚本（纯标准库，无需 pip install）：

| 脚本 | 作用 | 用法 |
|------|------|------|
| `scripts/sync_db.py` | SQLite 索引同步 | `python3 scripts/sync_db.py --incremental` |
| `scripts/lint_concepts.py` | 概念页格式质检 | `python3 scripts/lint_concepts.py --file 概念名` |

**脚本不是必须的。** 不装也能正常使用所有功能——只是索引需要手动维护，质检需要人工检查。

---

## 目录结构

```
concept-studio-spread/
├── SKILL.md                 # ← 改这里的一行配置就行
├── README.md                # 本文件
├── modules/
│   ├── page-spec.md         # 概念页格式规范（唯一权威）
│   ├── scholar-dict.json    # 学者名对照表
│   ├── parable.md           # 寓言故事模块
│   ├── ingest.md            # 概念摄入模块
│   ├── hop.md               # 概念跳跃模块
│   ├── roundtable.md        # 圆桌讨论模块
│   ├── analyze.md           # 关联分析模块
│   ├── cards.md             # 知识卡片模块
│   └── write-page.md        # 概念页写入层（共享模块，不被直接触发）
└── scripts/
    ├── sync_db.py           # SQLite 同步脚本
    └── lint_concepts.py     # 质检脚本
```

---

## 工作流示意

```
阅读/对话 → 发现有趣概念
    │
    ├─→ 「摄入」→ 自动建概念页 → 入库
    │
    ├─→ 「讲个寓言」→ AI 编故事 → 揭示原理 → 「建页」→ 入库
    │
    └─→ 「跳一跳」→ 已有概念 → 推荐 3 个新方向 → 「沉淀」→ 入库
                                                          │
                                            「更新图谱」→ 分析链接关系
                                                          │
                                            「圆桌讨论」→ 多视角深挖 → 归位到概念页
```

---

## 许可证

MIT License

---

## 贡献

Issue 和 PR 都欢迎。核心原则：
- 保持 `{ROOT}` 路径机制不动
- 新模块应在 `modules/` 下独立文件