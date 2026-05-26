---
name: clip-zh
description: Translate clipping articles to Chinese and save as a new markdown in Clippings. Use this whenever the user asks to "翻译", "中文化", "翻译这篇文章", "保存到 Clippings", or provides a clipping markdown file/link that should become a Chinese version.
version: "1.0"
updated: 2026-05-25
---

# clip-zh

将 Clippings 目录下的文章翻译为中文，并保存为新的 Markdown 文件。


## 本次流程总结

- 已完成从英文剪藏到中文稿的完整翻译与落盘。
- 根据反馈修正了命名策略：英文文件名保持英文，并在原文件名后追加 `_zh`。
- 对长篇 Transcript 按语义拆分章节，在原转录文本中插入章节标题，提升可读性与检索性。
- 保持 frontmatter、链接、图片与原始结构不破坏。

## 适用场景

在以下请求中优先使用本 skill：

- 用户要求把文章翻译成中文并保存
- 用户给出 Clippings 下的 `.md` 文件作为输入
- 用户要求保留 frontmatter、链接、图片、表格结构
- 来源是网页/视频剪藏，可能正文不完整

## 目标

- 产出一个新的中文 Markdown 文件（保存在 `Clippings/`）
- 尽量完整翻译正文
- 保留原文结构与可用元数据
- 对“无正文仅链接”场景给出明确说明，不编造内容

## 标准流程

1. 读取输入文件的完整内容（至少覆盖 frontmatter 与正文）。
2. 判断内容完整度：
   - 若有正文：执行完整翻译。
   - 若仅有标题/描述/链接（如 YouTube 链接）：只翻译可见信息，并在文中注明“当前无可翻译正文”。
3. 翻译策略：
   - 保留 YAML frontmatter 字段结构。
   - `title`、`description` 翻译为中文；`source`、`published`、`created`、`tags` 原样保留或最小必要调整。
   - 正文按原层级翻译，保留标题层级、表格、列表、链接、图片引用。
   - 若正文为长转录（Transcript），按内容语义分章，并将章节行插入原转录文本中（不改动时间戳与原段落顺序）。
4. 命名输出文件：
   - 若原文件名为英文：保持英文原名，在文件名后追加 `_zh`。
   - 示例：`The prompting playbook_zh.md`。
   - 若原文件名为中文：使用“中文标题 + `-zh`”。
   - 示例：`某篇文章-zh.md`。
   - 保存到 `Clippings/`，不覆盖原文件。
5. 保存并返回结果：
   - 明确告知新文件路径。
   - 若源内容不足，明确说明翻译范围限制。

## 输出要求

- 语言：简体中文。
- 风格：忠实、清晰、术语一致。
- 不添加原文没有的事实性内容。
- 不删除原文中的关键结构（标题、表格、链接、图片）。

## 质量检查清单

在保存前核对：

- frontmatter 语法正确（`---` 包裹，缩进合法）
- 中文标题与内容一致
- 链接和图片 URL 未破坏
- 表格列对齐可读
- 文件已写入 `Clippings/`

## 异常处理

- 输入文件不存在：提示用户确认路径。
- 仅有外链且无法获取正文：
  - 生成“可见信息翻译版”文件；
  - 在正文前添加简短说明，标明未获取到正文。
- 文件名冲突：在 `_zh` 或 `-zh` 后追加递增序号（如 `The prompting playbook_zh-2.md`、`某篇文章-zh-2.md`）。
