# 可编辑版本（Editable Variant）

每次渲染输出**两个文件**：

| 文件 | 用途 |
|---|---|
| `<姓名>-resume-<模板>.html` | 最终成品，打印 / 投递用 |
| `<姓名>-resume-<模板>-editable.html` | 浏览器里点字就能改的版本，用户自己微调用 |

可编辑版 = 在成品基础上加 3 处：① `<style>` 末尾追加编辑态样式 + 打印隐藏；② `<body>` 开头插入浮动工具条；③ 包内容的根 `<div class="page">` 加 `contenteditable="true"`。模板的视觉设计完全不动。

## 把任意成品 HTML 升级成 editable 的注入片段

**1. 在 `<style>` 的 `}` 闭合之前追加：**

```css
/* --- editable mode (hidden when printing) --- */
body { background: #f3f4f6; }
[contenteditable="true"]:hover { background: #fff7d6; outline: 1px dashed #d6b500; cursor: text; }
[contenteditable="true"]:focus { background: #fff; outline: 2px solid #2d6cdf; }
.toolbar {
  position: fixed; top: 12px; right: 12px; z-index: 999;
  background: #1a1a1a; color: #fff; padding: 10px 14px;
  border-radius: 10px; font: 12px/1.4 "Helvetica Neue", Arial, sans-serif;
  box-shadow: 0 8px 24px rgba(0,0,0,.18); display: flex; align-items: center; gap: 10px;
}
.toolbar small { color: #c9d1e0; font-size: 11px; }
.toolbar button {
  background: #2d6cdf; color: #fff; border: 0; padding: 6px 12px;
  border-radius: 6px; font-weight: 700; cursor: pointer; font-size: 11px;
}
.toolbar button:hover { background: #1a55c5; }
.toolbar button.ghost { background: transparent; border: 1px solid #555; }
@media print {
  body { background: #fff; }
  .toolbar { display: none !important; }
  [contenteditable="true"]:hover,
  [contenteditable="true"]:focus { background: transparent !important; outline: none !important; }
}
```

**2. 紧跟 `<body>` 之后插入工具条：**

```html
<div class="toolbar">
  <span><b>Edit mode</b> <small>· click any text to edit</small></span>
  <button onclick="window.print()">Save as PDF (⌘P)</button>
  <button class="ghost" onclick="document.querySelectorAll('[contenteditable]').forEach(el=>el.setAttribute('contenteditable', el.getAttribute('contenteditable')==='true'?'false':'true'));this.textContent=this.textContent==='Lock'?'Unlock':'Lock'">Lock</button>
</div>
```

**3. 给主容器加 `contenteditable`：**

```html
<div class="page" contenteditable="true" spellcheck="false">
```

> 把 `<title>` 也顺手改成 `... — Resume (editable)` 以便和成品区分。

## 行为约束

- **只是浏览器内编辑**：刷新会丢，必须告诉用户"改完直接 Cmd+P 存 PDF"才能落地
- **不替代结构化数据**：如果用户在编辑版里改了重要内容（数字、公司名），让他告诉你改了什么，同步回 `resume-data` 和成品文件
- **可选**：用户只要成品不要编辑版时，跳过本步骤

## 渲染流程触发点

在 `SKILL.md` 的渲染流程第 4 步保存文件之后，**自动同时生成 editable 版**并一起告知用户，让他自己决定要哪个。
