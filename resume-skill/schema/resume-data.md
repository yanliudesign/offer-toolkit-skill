# Resume Data — 标准结构化字段

所有入口（美化 / LinkedIn / 对话）都先把内容整理成下面这套字段，再去套模板。整理时用这个格式回显给用户确认。缺失项标 `[缺失]`，不确定的数字标 `[待确认]`。

```yaml
# ---- Header ----
name:            # 全名
headline:        # 一句话定位 / 目标职位，如 "Senior Backend Engineer"
location:        # 城市, 国家（可选，远程时可省）
email:
phone:           # 可选
links:           # 0-N 个，name + url
  - { name: LinkedIn, url: }
  - { name: GitHub,   url: }
  - { name: Portfolio,url: }

# ---- Summary（可选，3-4 行）----
summary:         # 定位 + 核心优势 + 想找什么，不写废话

# ---- Experience（倒序，最重要的板块）----
experience:
  - company:
    role:
    location:    # 可选
    start:       # YYYY-MM
    end:         # YYYY-MM 或 Present
    bullets:     # 每条：动词 + 做了什么 + 量化结果。见 guides/writing-tips.md
      - 
      - 

# ---- Projects（可选，学生/转行/工程师重要）----
projects:
  - name:
    role:        # 可选
    link:        # 可选
    date:        # 可选
    bullets:
      - 

# ---- Education ----
education:
  - school:
    degree:      # 学位 + 专业
    location:    # 可选
    start:       # 可选
    end:
    detail:      # 可选：GPA / 荣誉 / 相关课程

# ---- Skills ----
skills:          # 按组归类更专业
  - { group: Languages,  items: [ ] }
  - { group: Frameworks, items: [ ] }
  - { group: Tools,      items: [ ] }

# ---- 可选板块（没有就整块不要）----
certifications:  # name + issuer + date
awards:          # title + date + note
languages:       # language + level
publications:    # title + venue + date
volunteer:       # org + role + bullets
```

## 整理时的判断

- **板块取舍**：应届/转行 → 把 Projects、Education 提前；资深 → Experience 第一，Education 收到末尾一行。
- **时间格式统一**：全用 `YYYY-MM`（或 `YYYY`），不要混。`Present` 表示在职。
- **倒序**：Experience / Education / Projects 一律最近的在最上面。
- **数字必查**：bullet 里出现的任何百分比、金额、人数、时长，回显时单独列出来让用户确认，不确定就 `[待确认]`。
