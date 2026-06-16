# 通用简历 · Resume Builder Skill

一个 [Claude Code / Claude Agent Skill](https://docs.anthropic.com)，把零散的个人经历变成一份专业简历，并**一份数据导出 HTML / PDF / Word 三种格式**，内置 **ATS（简历筛选系统）通关**能力，适配任意岗位（技术 / 产品 / 运营 / 设计…）。

> A Claude skill that turns raw experience into a polished résumé and exports HTML / PDF / Word from a **single source of truth**, with built-in **ATS keyword alignment**. Works for any role.


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

