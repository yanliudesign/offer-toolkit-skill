---
name: resume-skill
description: "简历生成与美化 OS。两种入口：把已有简历(PDF/Word/文本)解析、诊断、套用模板美化；或者还没有简历时，通过 LinkedIn 导入或一问一答的对话帮你从零建出一份。输出单页打印优化的 HTML(浏览器里 Cmd+P 直接存成 PDF)，提供 4 套模板：Classic/ATS 友好、Modern 侧栏、Elegant 衬线、Tech 紧凑。关键词：resume, CV, 简历, 美化简历, 做简历, 简历模板, resume template, LinkedIn 简历, 求职简历, ATS, 改简历, polish resume。"
---

# Resume Skill — 简历生成与美化

把"我需要一份好看的简历"变成一条稳定流程：**所有素材先汇入一份标准化的结构化数据，再套模板渲染**。这样换模板只是换皮，内容不丢；美化和从零创建走的是同一条后半段。

## 三条第一原则

1. **绝不杜撰。** 所有经历、职责、数字都必须来自用户真实提供的内容。可以引导、追问、帮他把模糊的说清楚、把弱 bullet 改强，但绝不编造公司、职位、成果或量化数字。**任何数字都要向用户求证**，不确定就标记 `[待确认]` 而不是猜一个。
2. **一次只问一个问题。** 对话式建简历是访谈不是问卷。问一个 → 等回答 → 顺着追问。永远不要一次抛一串问题。
3. **先结构化，再渲染。** 不管入口是哪条，都先把内容整理成 `schema/resume-data.md` 定义的字段，确认无误后才套模板出 HTML。

---

## 路由：用户进来时先判断意图

| 用户说的话 | 走哪条流程 |
|---|---|
| "帮我美化简历" / "改简历" / 上传了一份已有简历(PDF/docx/txt/md) | **美化已有简历** → `prompts/beautify.md` |
| "我还没简历，这是我 LinkedIn" / 贴出 linkedin.com 链接 | **LinkedIn 导入** → `prompts/linkedin-import.md` |
| "我没有简历，帮我做一份" / "通过聊天帮我做" | **对话式建简历** → `prompts/interview.md` |
| "换个模板" / "这套不好看" | 已有结构化数据时，直接重渲染(见下方渲染流程) |

判断不了就问一句：
> "你是**已经有一份简历想美化**，还是**从零开始做一份**？从零的话，你更想**贴 LinkedIn 链接**让我导，还是**咱们聊一聊**我帮你问出来？"

---

## 美化已有简历

详见 `prompts/beautify.md`。要点：

1. **读取**用户提供的简历(可读 PDF / 复制粘贴的文本 / Word 导出)。Claude 可直接 Read PDF。
2. **解析**进 `schema/resume-data.md` 的字段，缺失项标 `[缺失]`。
3. **诊断**(对照 `guides/writing-tips.md`)：哪些 bullet 没有量化结果、哪些是职责堆砌而非成果、排版/长度/时间线问题、ATS 风险。给出一份简短诊断清单。
4. **征求同意再改内容**：问用户"我可以顺手把这几条弱 bullet 改强吗？(不改事实，只改表达)"。用户同意才改，且改完逐条让其确认数字。
5. **选模板 → 渲染**(见下方)。

---

## LinkedIn 导入

详见 `prompts/linkedin-import.md`。要点：现实是 LinkedIn 有登录墙，直接抓公开 URL 经常被拦。流程会先尝试 WebFetch，拿不到就引导用户用 LinkedIn 的"Save to PDF"导出个人资料或复制粘贴各板块内容，再解析进 schema。

---

## 对话式建简历

详见 `prompts/interview.md`。一问一答，按 联系方式 → 目标岗位 → 每段经历(公司/职位/时间 → 做了什么 → 成果数字) → 教育 → 技能 的顺序，挖一段结构化一段，最后汇总进 schema。

---

## 渲染流程（三条入口共用的后半段）

1. **确认结构化数据**：把整理好的 `resume-data` 内容回显给用户，确认无误（尤其数字）。
2. **选模板**：11 套，问用户偏好（默认推荐 Classic/ATS，因为海投最稳）：
   | 模板 | 文件 | 适合 | ATS |
   |---|---|---|---|
   | **Classic / ATS** | `templates/classic-ats.html` | 单栏无花哨，机器可解析，大公司海投最稳 | ✅ 友好 |
   | **Ledger 学术工程** | `templates/ledger.html` | LaTeX 风衬线，公司/日期两端对齐，嵌套子弹，软件/数据/工程岗 | ✅ 友好 |
   | **Tech 紧凑** | `templates/tech-compact.html` | 高信息密度+等宽点缀，工程师把多项目塞进一页 | 🟡 尚可 |
   | **Modern 侧栏** | `templates/modern-sidebar.html` | 双栏+深色侧边栏，现代感强 | 🟡 一般 |
   | **Pillar 信息卡** | `templates/pillar.html` | Enhancv 风，蓝点缀+技能胶囊+图标成就+语言进度点，产品/市场/PM | 🟡 一般 |
   | **Elegant 衬线** | `templates/elegant-serif.html` | 衬线居中编辑风，设计/咨询/市场等偏人文岗 | 🟡 一般 |
   | **Atelier 极简** | `templates/atelier.html` | 大量留白+细字大写名+竖线分栏，设计/创意/审美岗 | 🟡 一般 |
   | **Timeline 时间轴** | `templates/timeline.html` | 左侧竖向时间轴脊柱，一眼看出职业成长轨迹 | 🟡 一般 |
   | **Swiss 栅格** | `templates/swiss.html` | 瑞士栅格，粗体 Helvetica + 红点缀，设计/品牌/创意 | 🟡 一般 |
   | **Executive 高管** | `templates/executive.html` | 藏青衬线，稳重有分量，金融/咨询/高管/资深领导 | 🟡 一般 |
   | **Color-block 色块头** | `templates/colorblock.html` | 顶部整宽珊瑚色块，现代大胆，互联网/营销/年轻求职者 | 🟡 一般 |

   选模板提示：**海投/过机器筛 → Classic/ATS 或 Ledger**；**人直接看/内推/作品集向 → 其余几套更出彩**。
3. **渲染**：读取选定模板，**保留其 `<style>` 不动**，把示例内容替换成用户的真实数据，删掉用不到的板块（模板里每个 `<section>` 可整块删）。生成一个自包含的单文件 HTML。
4. **同时输出可编辑版**：再生成一份 `<姓名>-resume-<模板>-editable.html`，加上 `contenteditable` + 浮动工具条（详见 `prompts/editable-version.md`）。打印时编辑高亮和工具条自动隐藏，PDF 输出干净。
5. **输出**：两个文件都保存为 `<姓名>-resume-<模板>.html` 和 `<姓名>-resume-<模板>-editable.html`。按用户全局偏好默认存到 `/Users/yanliu/Desktop/Claude skills/`（其他用户则存当前目录或询问）。
6. **告诉用户怎么转 PDF**：浏览器打开 → `Cmd+P` → 目标选"另存为 PDF" → 边距设 None/Default、勾选背景图形 → 保存。editable 版可以先在浏览器里点字微调再 `Cmd+P`，工具条上有现成按钮。
7. **可换模板重渲染**：结构化数据已在手，用户说"换 Modern 试试"就直接读另一套模板重渲染，无需重新采集。

---

## 渲染时的硬规则

- **一页优先**：经验 <10 年应控制在 1 页；资深可 2 页。内容超了优先精简 bullet，不要缩到看不清。
- **不动模板 CSS**：模板的版式/配色是设计好的，只替换内容文本。用户想调色再单独问。
- **空板块整块删**：没有的板块（如 Publications）连同 `<section>` 一起删，不要留空标题。
- **真实数据**：任何示例里的 placeholder 数字都必须换成用户真实数据或 `[待确认]`，绝不把模板示例数字留在成品里。
- **联系信息脱敏提醒**：如果用户要公开分享，提醒电话/地址是否需要打码。

---

## 配套文件

- `schema/resume-data.md` — 标准结构化字段（所有流程的中转格式）
- `prompts/interview.md` — 对话式采集脚本
- `prompts/linkedin-import.md` — LinkedIn 导入与降级方案
- `prompts/beautify.md` — 已有简历解析与诊断
- `prompts/editable-version.md` — 把成品升级成浏览器可编辑版的注入片段
- `guides/writing-tips.md` — bullet 写法、量化、ATS 关键词、常见错误
- `templates/*.html` — 11 套打印优化模板
