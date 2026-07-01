# LinkedIn 导入

目标：把用户的 LinkedIn 个人资料变成 `schema/resume-data.md`。**现实约束：LinkedIn 有登录墙，直接抓公开 URL 经常被 403/拿到空壳。** 所以流程是"先试，拿不到就优雅降级"。

## 步骤

### 1. 先尝试直接抓
用户贴了 `linkedin.com/in/...` 链接时，用 WebFetch 试一次，提取姓名、headline、经历、教育、技能。

### 2. 抓不到就降级（大概率走这条）
被拦 / 内容残缺时，**不要硬刚**，直接给用户两个简单选项：

> "LinkedIn 不让程序直接读你的资料（需要登录）。两个办法，挑一个——
> **(A) 导出 PDF（推荐，最全）**：电脑上打开你的 LinkedIn 主页 → 头像下方的 **Resources / More** → **Save to PDF**，把生成的 PDF 发我，我直接读。
> **(B) 复制粘贴**：把你资料页的 About、Experience、Education、Skills 几块文字复制下来发我就行。"

- 用户发来 PDF → 直接 Read PDF 解析。
- 用户粘贴文本 → 直接解析。

### 3. 解析进 schema
把抓到/拿到的内容映射进 `schema/resume-data.md` 的字段：
- LinkedIn 的 "About" → `summary`
- 每段 "Experience" → `experience[]`（公司/职位/时间/描述拆成 bullets）
- "Education" → `education[]`
- "Skills" → `skills`（帮他分组）
- "Licenses & certifications" → `certifications`

### 4. 补强 + 求证
LinkedIn 的经历描述往往是段落、缺量化。导入后：
- 把段落拆成 bullet，按 `guides/writing-tips.md` 的"动词+成果"重写。
- **凡是没有数字的成果，标 `[待确认]` 并问用户**："你 LinkedIn 这段没写数字，这块业务大概影响多少用户 / 提升多少？没有也没关系，我就不放数字。"
- 不替用户发明任何 LinkedIn 上没有、用户也没确认的内容。

### 5. 进渲染流程
确认结构化数据（尤其数字）→ 选模板 → 出 HTML。
