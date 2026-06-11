---
name: 通用简历
description: 通用简历撰写与多格式导出。输入基本信息 + 实习/项目经历（任意岗位），AI 扫描结构化并按 XYZ 量化法编写，做 ATS 关键词对齐与体检，一键导出 PDF / Word / HTML 三格式（蓝白视觉版 + ATS 安全版）。触发场景：用户说"写简历""做简历""生成简历""简历模板""导出简历 PDF/Word"，或提供个人信息+经历让你做简历。
user_invocable: true
---

# 通用简历撰写器

一份数据 → 三格式输出，内置 ATS 通关能力，适配任意岗位（技术/产品/运营/设计…）。方法论受 ComposioHQ/awesome-claude-skills 的 Tailored Resume Generator 启发（inspired by），脚本/Schema/ATS 引擎/多格式渲染均为原创实现。

## 工作流（核心：单一数据源 resume.json）

```
① 收集：基本信息 + 教育 + 实习 + 项目 + 技能 + 荣誉（缺则逐项问）+ 目标岗位/JD
② AI 结构化 + 改写 → 写出 resume.json（套 methodology + metrics + 岗位关键词）
②.5 ATS 通关引擎：JD 关键词对齐 + 命中率评分 + 排版合规 → 出 ATS 体检报告（见 references/ats.md）
③ 渲染：python3 scripts/render.py resume.json → PDF / Word / HTML（visual + ats 两版）
```

**为什么要 resume.json 中间层**：AI 只负责把烂经历写成好内容并填进 JSON；三格式由脚本从同一份 JSON 渲染 → 内容天然一致、换模板不动内容。

## 默认段落顺序（校招）
基本信息 · 教育背景 · 实习经历 · 项目经历 · 专业技能 · 荣誉奖项
（社招把 internships 提到 education 前：改 `meta.section_order`）

## 怎么用

1. **收集信息**：让用户给 基本信息（姓名/意向/联系方式/GitHub）、教育、实习、项目、技能、荣誉、**目标岗位或 JD**。缺哪项逐项问；经历模糊就用 `references/metrics.md` 的引导问句逼出量化。
2. **写 resume.json**：照 `schema/resume.schema.json` 结构填；bullet 用 XYZ 量化法（`references/methodology.md`），技能/项目用 JD 原词对齐（`references/roles/`）。bullet 内可用 `**加粗**` 标量化结果。
3. **跑 ATS 体检**：按 `references/ats.md` 拆 JD、算命中率、补缺失（真有的嵌入、没有的标 gap 不造假），出体检报告给用户。
4. **渲染导出**：
   ```bash
   # 视觉版（投牛客站内 / 发人看 / 打印）→ 三格式
   python3 ~/.claude/skills/通用简历/scripts/render.py <resume.json> --out ~/Desktop --formats html,pdf,docx --style visual
   # ATS 安全版（投大厂官网 / 邮箱）
   python3 ~/.claude/skills/通用简历/scripts/render.py <resume.json> --out ~/Desktop --formats pdf,docx --style ats
   ```
   输出：`简历_<姓名>_<style>.pdf` / `_<style>.docx` / `_<style>.html`（文件名带 style，visual/ats 不互相覆盖）
   > PDF 依赖本机 Chrome；脚本会自动探测，找不到时可设环境变量 `RESUME_CHROME=/path/to/chrome`。
5. **出稿自查**：过一遍 `references/checklist.md`。

## 物料库（references/ 与 schema/、scripts/）
- `schema/resume.schema.json` — 数据结构（单一数据源）
- `references/methodology.md` — XYZ 量化法、动词库、岗位类型分支、Do/Don't、校招vs社招
- `references/metrics.md` — 量化锚点 + 引导问句
- `references/ats.md` — ATS 通关引擎（对齐评分 + 排版合规 + 两版 + 诚信红线）
- `references/checklist.md` — 出稿体检清单
- `references/roles/` — 岗位关键词库（后端/前端/算法AI/产品/运营 + JD 现场抽取兜底）
- `scripts/render.py` — json → HTML / PDF / Word
- `examples/resume.example.json` — 可直接跑的样例

## 红线
真实不造假（编造夸大面试必崩）；ATS 只做真实对齐不堆砌作弊；校招 1 页；投 ATS 渠道一律用 `--style ats`。

## 依赖
- PDF：本机 Chrome（headless 打印）
- Word：`python-docx`（缺则 `pip3 install python-docx`）
