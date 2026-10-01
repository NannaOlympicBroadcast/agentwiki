# AgentWiki

输入一个主题，自动搜索网络、整理信息，生成图文并茂的结构化 HTML 维基页面，并提供预览。

本仓库是一个 **Claude 插件**（Claude Code / Claude 桌面端 Cowork 均可使用），同时也是一个 marketplace，插件名为 `agentwiki`，包含一个 skill：`agentwiki`。

## 安装

### 方式一：通过 marketplace 安装（推荐）

在 Claude Code 中依次执行：

```
/plugin marketplace add NannaOlympicBroadcast/agentwiki
/plugin install agentwiki@agentwiki
```

> 本仓库当前为私有仓库，需要本机 Git 已登录有权访问该仓库的 GitHub 账号（例如先执行 `gh auth login`）。

### 方式二：本地目录加载

```
git clone https://github.com/NannaOlympicBroadcast/agentwiki.git
claude --plugin-dir ./agentwiki
```

### 方式三：只安装 skill

把 `skills/agentwiki` 整个目录复制到 `~/.claude/skills/`（个人级）或项目的 `.claude/skills/`（项目级）即可。

## 使用

安装后直接对 Claude 说，例如：

- “生成维基页面：特斯拉 Model 3”
- “百科介绍一下 RISC-V”
- “主题详解：南京大学”

也可以显式调用：`/agentwiki:agentwiki <主题>`。

## 工作流程

1. 用 WebSearch 搜索主题的定义、历史、特点等信息
2. 用 WebFetch 抓取关键网页
3. 整合关键事实与数据
4. 优先引用网页上的真实图片（官网、百科），必要时下载到本地后嵌入页面
5. 基于 `templates/wiki_template.html` 生成页面，保存为 `<项目根目录>/workipedia/[主题].html`
6. 启动本地 HTTP 服务并提供预览链接

## 目录结构

```
.
├── .claude-plugin/
│   ├── plugin.json          # 插件清单
│   └── marketplace.json     # marketplace 清单
├── skills/
│   └── agentwiki/
│       ├── SKILL.md         # skill 说明与工作流程
│       └── templates/
│           └── wiki_template.html
└── README.md
```

## 注意事项

- 输出为完整 HTML，不输出 Markdown。
- 预览步骤依赖运行环境中的端口暴露/网页预览工具；没有该工具时，直接打开生成的 HTML 文件即可。

## 许可证

[MIT](LICENSE)
