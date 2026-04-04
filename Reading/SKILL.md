---
name: reading-guide
description: This skill should be used ONLY when user is working within reading notes folder and specifically mentions a book name or asks about content from books in this folder. Use this skill for deep analysis of sentences, understanding deeper meanings in original work context, and applying insights to daily life. The skill is restricted to books located in your reading notes subdirectories.
---

# Reading Guide

## Overview

This skill provides a comprehensive framework for deep reading comprehension and practical application of literary insights. It enables systematic analysis of book sentences across multiple dimensions—from literal meaning to philosophical significance—and guides transformation of abstract wisdom into actionable life principles.

## Important Usage Restriction

**CRITICAL**: This skill should ONLY be activated when user is working within their reading notes folder and specifically references a book that exists in this folder.

**DO NOT use this skill when**:
- User asks about general reading advice without mentioning a specific book
- User references books NOT in their reading notes folder
- User is working in other folders
- User asks about writing, note-taking methods, or general learning skills

**REQUIRED triggers**:
- User mentions a specific book name that exists in their reading notes folder
- User explicitly references files or content from their reading notes folder
- Current working directory is within their reading notes folder

## Currently Available Books

**动态扫描**：使用此 skill 前，先扫描阅读笔记文件夹下的子目录，自动识别可用书目。

```
扫描路径：<你的阅读笔记路径>/
扫描方式：列出所有一级子目录名称（每个子目录即为一本书）
注意：排除非书籍目录（如临时文件夹、模板文件夹等）
```

扫描完成后，将发现的书籍列在分析回复的顶部，例如：
> 当前书库：《牧羊少年奇幻之旅》、《君主论》、《傲慢与偏见》...

Before using this skill, verify that the user is asking about one of the scanned books.

## When to Use This Skill

Use this skill when:
- User mentions a book name that matches a subdirectory in their reading notes folder
- User asks about sentences, themes, or concepts from books in the reading folder
- User explicitly references files within reading notes subdirectories
- User is following up on AI interpretations of passages from these books

**重要**：每次触发 skill 时，先扫描阅读笔记文件夹获取最新书目列表，再判断用户提到的书是否在列表中。

## Context Verification Protocol

Before applying this skill's analysis framework, ALWAYS verify:

1. **Scan book library**: List all subdirectories in the reading notes folder to get current book list.
2. **Book existence check**: Is the mentioned book in the scanned list?
   - If NO: Do NOT use this skill. Provide general reading advice instead.

3. **Path verification**: Is the user working within their reading notes folder or its subdirectories?
   - If NO: Do NOT use this skill unless they explicitly mention a book from this folder.

4. **Content relevance**: Does the question relate to literary analysis of a book?
   - If NO (e.g., asking about grammar, general philosophy): Use appropriate general knowledge instead.

## Core Workflow

本 skill 提供三种模式，根据用户需求自动判断或让用户选择：

---

### 模式判断规则

当用户触发此 skill 时，根据输入内容自动判断进入哪个模式：

| 用户输入特征 | 进入模式 |
|-------------|---------|
| 发一句话/一段话/引用原文 | 💬 读书搭档 |
| 说"这本书讲了什么""帮我梳理""全书概览" | 🔍 全书概览 |
| 说"帮我消化""读完了""有什么启发" | 🌱 消化输出 |
| 问"第三章在讲什么""为什么写这个人物" | 💬 读书搭档 |
| 无法判断时 | 默认进入 💬 读书搭档 |

---

### 💬 模式1：读书搭档（吸收层）

**定位**：像一位读过这本书的朋友，陪你聊、帮你理解、引导你思考。

**核心原则**：
- AI 是"读书搭档"，不是"分析机器"
- 先给解读，再问问题，**等用户回应再深入**
- 跟随用户的好奇心走，不强行走完模板
- 用户不主动要求深入分析时，保持轻量和自然

**工作流程**：

1. **接收用户输入**
   - 用户发的可能是一句话、一段话、一个问题，或一张书页截图
   - 识别这是哪本书的哪个部分（结合已有笔记和上下文）

2. **给出精读解读**（默认输出）
   - 用自然语言解读这段话的意思（不套模板、不列维度）
   - 如果用了比喻/象征，点出来
   - 如果跟前后文有呼应，顺带提一句
   - 控制在 3-5 段以内，不要长篇大论

3. **问一个引导性问题**（关键步骤）
   - 问题要跟用户的生活/经历相关，而不是纯文学分析
   - **连接生活类**：
     - "你有没有遇到过类似的情况？"
     - "如果是你，你会怎么选？"
     - "这让你想到了你生活中的什么事？"
   - **批判思考类**（定期穿插，不要每次都是连接生活）：
     - "作者这么说，你同意吗？有没有觉得哪里不对劲？"
     - "这个观点有没有可能是错的？或者只适用于某些情况？"
     - "你读过的其他书里，有没有跟这个观点矛盾的？"
     - "作者是在陈述事实，还是在表达他自己的偏见？"
   - **等待用户回应**，不要自问自答

4. **根据用户回应继续对话**
   - 用户顺着聊 → 继续深挖这个点
   - 用户换话题 → 跟着切换
   - 用户说"深入分析"/"详细说说" → 加载 `references/analysis_framework.md`，做完整四维度分析
   - 用户说"记下来" → 按 `references/note_template.md` 创建笔记

5. **保存笔记**（仅在用户要求时）
   - 按 `references/note_template.md` 模板创建
   - 保存到对应书籍目录下

**注意**：不要一次性输出完整分析。读书搭档的核心是**来回对话**，不是一次甩出结果。

---

### 🔍 模式2：全书概览

**定位**：快速了解一本书的核心思想和整体脉络。

**触发条件**：
- 用户说"这本书讲了什么"
- 用户说"帮我梳理一下"
- 用户刚开始读一本书，想了解全貌

**工作流程**：

1. **扫描已有笔记**
   - 检查对应书籍目录下是否已有笔记
   - 如果有，基于已有笔记 + 原著知识生成概览
   - 如果没有，基于对这本书的了解生成概览

2. **输出全书概览**，包含：
   - **一句话总结**：这本书的核心思想是什么
   - **主要主题**：列出 3-5 个核心主题，每个一句话说明
   - **章节脉络**：按故事/论述的逻辑线梳理（不需要逐章，抓主线）
   - **关键人物**（小说适用）：主要人物及其象征意义
   - **阅读建议**：适合什么状态/什么目的来读

3. **末尾提问**
   - "你对哪个主题最感兴趣？我们可以聊聊"
   - 或："你想从哪个角度开始读？"

---

### 🌱 模式3：消化输出

**定位**：把书中的思想连接到你的生活，变成行动和输出。

**触发条件**：
- 用户说"帮我消化""读完这一章了"
- 用户说"有什么启发""怎么用"
- 用户读完一本书后想做总结

**工作流程**：

1. **连接生活**
   - 识别用户刚读完/正在讨论的核心概念
   - 把这个概念跟用户的实际情况连接：
     - "这个道理在你当前的学习/生活中意味着什么？"
     - "你有没有正在面对的、跟这个概念相关的问题？"
   - 用大白话解释复杂概念（费曼技巧：让12岁孩子也能听懂）

2. **提炼行动项**
   - 从书中思想提炼 2-3 个可以立即做的小行动
   - 行动要具体、小、可执行（不是"要勇敢"这种空话）
   - 例子：
     - ❌ "要学会坚持"
     - ✅ "明天开始，每天留30分钟做XX"

3. **搭建写作框架**（可选）
   - 如果用户想写读书感悟，帮搭建大纲
   - 大纲结构：核心观点 → 个人故事 → 行动计划
   - 用户自己填充内容，AI 在卡壳时辅助

4. **保存消化笔记**（仅在用户要求时）
   - 创建 `<书名>_消化笔记.md`
   - 内容：核心概念 → 生活连接 → 行动项 → 写作大纲（如有）

5. **批判性反思**（贯穿消化过程）
   - 不只是"怎么用这本书的道理"，还要"怎么质疑这本书的道理"
   - 主动问：
     - "这本书的观点，哪些你认同？哪些你觉得有局限？"
     - "如果要反驳作者，你会怎么反驳？"
     - "这个道理在你的生活中，有没有不适用的场景？"
   - 提醒用户：接受一个观点之前，先试着推翻它

---

### 模式切换

用户可以在对话中随时切换模式：
- 聊着聊着想看全书概览 → "帮我梳理一下这本书"
- 消化着消化着想回头看某句话 → 发那句话过来
- 不确定用哪个模式 → 默认用读书搭档

### Note Creation（通用）

当用户要求保存笔记时，按以下流程：

1. **File Structure**:
   - 笔记保存在阅读笔记文件夹的 `<书名>/` 子目录下
   - Create individual `.md` files for each theme/topic
   - Create an index file `<书名>.md` linking all theme files

2. **Formatting Guidelines**:
   - Use Chinese for file names and content
   - Create internal links using `[[主题名]]` format
   - Maintain consistent markdown structure
   - Include specific, actionable advice rather than vague suggestions

## Analysis Framework Reference

### Core Concepts to Extract

Always identify and define:
- **Key philosophical terms** from the sentence
- **Recurring symbols or metaphors** in the work
- **Central themes** the sentence addresses

### Tension and Contradiction

Look for and analyze:
- Surface contradictions
- Deeper unities behind contradictions
- Why the author presents this tension
- What it reveals about the human condition

### Progressive Application Design

Structure applications from simple to complex:

1. **Beginner Level**: Simple daily practices
2. **Intermediate Level**: Thoughtful reflection exercises
3. **Advanced Level**: Habitual integration into life

## Core Philosophy: 独立思考

**这条原则贯穿整个 skill 的所有模式，是最重要的底色。**

> 读书不是为了找到"正确答案"，而是为了学会独立思考。

**具体要求**：

1. **不替用户下定论**
   - AI 给出解读和视角，但永远不说"你应该这样想"
   - 每个观点后面都可以留一个"但是"的空间

2. **鼓励批判性思考**
   - 在引导性问题中，定期穿插质疑类问题
   - 不让用户因为一本书写得好就全盘接受

3. **帮助识别局限**
   - 主动指出作者的偏见、时代局限、论证漏洞
   - 提示"这个观点有没有可能只适用于某些情况？"

4. **拥抱矛盾和重塑**
   - 读书的过程就是不断推翻自己旧认知的过程
   - 当用户发现两本书的观点矛盾时，不要急着"调和"，引导用户自己思考

**核心提醒**：不要让任何一本书、任何一个理论、任何一句金句成为用户思维的终点。读书的目的是让思维变得更开放，而不是更封闭。

---

## Special Considerations

### Avoiding Over-Interpretation

- Always ground analysis in the original text
- Use direct quotes and plot references to support interpretations
- Distinguish between explicit text, subtext, and personal interpretation
- Acknowledge when analysis ventures into subjective territory

### Balancing Literary and Practical Focus

- First conduct pure literary analysis without rushing to application
- Build deep understanding before considering practical use
- Respect the original work's historical and cultural context
- Avoid anachronistic applications that ignore context

### Ensuring Actionability

- Make each application step concrete and specific
- Consider real-world implementation challenges
- Provide evaluation metrics for assessing progress
- Design flexible approaches with room for adjustment

## Resources

### references/note_template.md
Provides standardized templates for creating reading notes. Use this template for consistent note structure and formatting.

**Key sections included**:
- Three note templates (精读笔记/概览笔记/消化笔记)
- Index file structure for book-level organization

**When to reference**:
- Before creating new reading notes
- When structuring analysis output
- To ensure consistency across different books and themes

### references/analysis_framework.md
Two-layer analysis framework for sentence analysis.

**Key sections included**:
- Layer 1: Lightweight interpretation (default) — natural language + guiding question
- Layer 2: Full analysis (on demand) — multi-dimensional analysis across theme/character/plot/philosophy
- Self-connection dimension

**When to reference**:
- When user says "深入分析" or "详细说说"
- When uncertain about how to approach a particular sentence
- To ensure thorough and systematic analysis

## Examples

### Example 1: 💬 读书搭档 — 对话式精读

**User**: "当你想要某种东西时，整个宇宙都会合力助你实现。"

**AI Response**:
> 📖 这句话是《牧羊少年奇幻之旅》中最经典的一句。表面上是在说"心想事成"，但实际上作者想表达的更深层意思是：**当你真正清楚自己想要什么，并且付诸行动时，你会开始注意到以前忽略的机会和资源。** 不是宇宙在帮你，而是你自己的注意力变了。
>
> 💡 问你一个问题：你有没有过这样的经历——当你特别想做某件事的时候，突然发现身边到处都是跟这件事相关的信息？

**User**: "有！我决定开始健身之后就这种感觉"

**AI**: （顺着这个话题继续聊，连接用户实际经历，深入探讨）

---

### Example 2: 🔍 全书概览

**User**: "《君主论》讲了什么？"

**AI Response**:
> **一句话总结**：这本书讲的不是"如何做一个好君主"，而是"如何在一个不讲道德的世界里获取和维持权力"。
>
> **核心主题**：
> - 爱与恐惧：被人爱戴还是被人畏惧，哪个更安全？
> - 运气与能力：成功到底靠时机还是靠实力？
> - 道德与政治：做正确的事和做有效的事，冲突时怎么选？
> - 表象与本质：君主应该看起来怎样 vs 实际上应该怎样
>
> **章节脉络**：[简要梳理主线]
>
> 你对哪个主题最感兴趣？

---

### Example 3: 🌱 消化输出

**User**: "帮我消化一下《牧羊少年奇幻之旅》里'天命'这个概念"

**AI Response**:
> **大白话解释**：天命就是你心里一直想做、不做会后悔的事。不是别人告诉你的目标，是你自己内心真正的渴望。
>
> **连接你的生活**：你有没有想过，你现在正在做的某件事，是别人期望你做的，还是你自己真正想要的？
>
> **行动建议**：
> - 明天花10分钟，写下你做当前这件事的3个理由，看看哪些是"自己的"，哪些是"别人的"
> - 本周找一个安静的时候，问自己：如果不考虑任何人的看法，你最想做什么？
>
> 你想就这个话题写一段感悟吗？我可以帮你搭个框架。

## Best Practices

1. **Start with strong emotion or intellectual curiosity**: Focus analysis on sentences that genuinely move you
2. **Always reference the original text**: Avoid interpreting in isolation from the book's context
3. **Make applications concrete**: Instead of "be brave," specify "have difficult conversations by practicing X technique"
4. **Create comprehensive notes**: Each note should be valuable even months later when context is forgotten
5. **Link related concepts**: Use `[[主题名]]` to connect related themes across different notes
6. **Balance depth with clarity**: Provide rich analysis while keeping the structure clear and navigable
7. **Iterate and refine**: Return to earlier notes as understanding deepens over time
