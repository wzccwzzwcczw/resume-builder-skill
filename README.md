# 通用简历 · Resume Builder Skill

一个 [Claude Code / Claude Agent Skill](https://docs.anthropic.com)，把零散的个人经历变成一份专业简历，并**一份数据导出 HTML / PDF / Word 三种格式**，内置 **ATS（简历筛选系统）通关**能力，适配任意岗位（技术 / 产品 / 运营 / 设计…）。

> A Claude skill that turns raw experience into a polished résumé and exports HTML / PDF / Word from a **single source of truth**, with built-in **ATS keyword alignment**. Works for any role.

## ✨ 特性

- **单一数据源**：所有内容写进一份 `resume.json`，三种格式由脚本渲染 → 内容天然一致，换模板不动内容
- **三格式导出**：HTML / PDF / Word，一条命令出齐
- **两种风格**：`visual`（蓝白视觉版）+ `ats`（单栏纯净、可被 ATS 正确解析）
- **ATS 通关引擎**：JD 关键词对齐 + 命中率评分 + 排版合规 +「不堆砌作弊」诚信红线
- **写作方法论内置**：XYZ 量化法、动词库、量化引导问句、岗位关键词库、出稿体检清单
- **通用**：JD 现场抽取兜底任意岗位，预置后端/前端/算法AI/产品/运营等高频方向

## 🚀 安装

把整个 `通用简历/` 文件夹放到你的 Claude skills 目录：

```bash
# macOS / Linux
cp -r 通用简历 ~/.claude/skills/
```

依赖：

```bash
pip install -r requirements.txt          # python-docx（Word 导出）
# PDF 导出需本机 Chrome/Chromium（脚本自动探测；找不到设 RESUME_CHROME=/path/to/chrome）
```

## 📦 用法

### 在 Claude 里（推荐）
直接说「帮我写简历 / 做一份 Agent 开发简历」，skill 会逐项收集信息、按 XYZ 量化法成稿、做 ATS 体检并导出三格式。

### 命令行直接渲染
```bash
# 视觉版（投递平台站内 / 打印 / 发人看）→ 三格式
python3 scripts/render.py examples/resume.example.json --out ~/Desktop --formats html,pdf,docx --style visual

# ATS 安全版（投大厂官网 / 邮箱）
python3 scripts/render.py examples/resume.example.json --out ~/Desktop --formats pdf,docx --style ats
```
输出：`简历_<姓名>_<style>.pdf / .docx / .html`

## 🗂 结构

```
通用简历/
├── SKILL.md                      # 工作流 + 用法（Claude 读取）
├── schema/resume.schema.json     # 简历数据结构（单一数据源）
├── scripts/render.py             # json → HTML / PDF / Word
├── references/
│   ├── methodology.md            # XYZ 量化法、动词库、校招 vs 社招
│   ├── metrics.md                # 量化锚点 + 引导问句
│   ├── ats.md                    # ATS 通关引擎
│   ├── checklist.md              # 出稿体检清单
│   └── roles/README.md           # 岗位关键词库
└── examples/resume.example.json  # 可直接跑的样例
```

## ⚠️ 红线

真实不造假（编造夸大面试必崩）；ATS 只做真实关键词对齐，**不做白字堆砌作弊**；校招控制 1 页；投 ATS 渠道一律用 `--style ats`。

## 🙏 致敬

方法论部分 **inspired by** [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) 的 *Tailored Resume Generator*。本仓库的脚本、数据 Schema、ATS 引擎、多格式渲染与中文 + 通用化适配均为原创实现。

## 📄 License

[MIT](./LICENSE) — 记得把 `LICENSE` 里的版权人改成你自己。
