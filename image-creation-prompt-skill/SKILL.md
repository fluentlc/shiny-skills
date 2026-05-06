---
name: image-creation-prompt-skill
description: Use when user wants to create an AI image with a specific style — takes a simple Chinese/English description (topic + style + aspect ratio) and transforms it into an optimized, structured prompt using proven style templates. Trigger on phrases like "生成一张...图片", "创建...风格图片", or any image creation request with a style name.
---

# Shiny Image Creation Prompt Skill

## Overview

Transforms simple image creation requests into detailed, structured prompts optimized for AI image generators (Banana2, Banana Pro, Midjourney, DALL-E, Stable Diffusion, etc.). Style templates are stored in `styles/` and loaded on demand — only the matched style enters context.

## Input Parsing

User input format (flexible): `[topic], [style], [aspect ratio]`

Examples:
- `生成一张从Function Call到MCP到SKILL的发展历程图片，哆啦A梦风格，16:9`
- `创建一张微服务架构图，黑板报风格，4:3`
- `画一张AI学习路线，手绘涂鸦风格`

Parse into:
- **topic**: The subject/concept to visualize
- **style**: Match against the Style Registry below
- **aspect_ratio**: Default `16:9` if not specified

## Generation Process

1. **Parse** user input → extract topic, style, aspect ratio
2. **Match** style name/keywords → find entry in Style Registry
3. **Load** the matched style file using the Read tool
4. **Decompose** topic into 3–5 logical steps or content sections
5. **Fill** template with topic-specific content (labels, descriptions, visuals, dialogue)
6. **Output** the complete structured prompt as a single code block

## Style Registry

| Style Name                           | Keywords                                 | File                               |
| ------------------------------------ | ---------------------------------------- | ---------------------------------- |
| 哆啦A梦风格 (Doraemon)                    | 哆啦A梦、doraemon、藤子、漫画角色                    | `styles/doraemon.md`               |
| 简约手绘涂鸦插画风格 (Doodle)                  | 手绘、涂鸦、doodle、插画、素描                       | `styles/doodle.md`                 |
| 黑板报风格 (Chalkboard)                   | 黑板、粉笔、chalkboard、黑板报                     | `styles/chalkboard.md`             |
| 吉伊卡哇风格 (Chiikawa)                    | 吉伊卡哇、chiikawa、ちいかわ、治愈                    | `styles/chiikawa.md`               |
| 蜡笔小新搞怪涂鸦风格 (Shin-chan)               | 蜡笔小新、小新、shin-chan、搞怪涂鸦                   | `styles/shinchan.md`               |
| 复古怀旧手绘插画风格 (Vintage Sketchnote)      | 复古、怀旧、vintage、sketchnote、手绘插画            | `styles/vintage-sketchnote.md`     |
| 黏土定格动画风格 (Claymation)                | 黏土、定格动画、claymation、clay                  | `styles/claymation.md`             |
| 美式波普漫画风小红书插图风格 (Pop Art Xiaohongshu) | 波普、漫画、小红书、pop art、xiaohongshu            | `styles/pop-art-xiaohongshu.md`    |
| 美式超级英雄漫画风格 (Superhero Comic)         | 超级英雄、漫威、DC、marvel、superhero、comic        | `styles/superhero-comic.md`        |
| 动漫人物手捧本尊手办风格 (Anime Figurine)        | 手办、cosplay、figurine、本尊手办                 | `styles/anime-figurine.md`         |
| 物品爆炸视图风格 (Exploded View)             | 爆炸视图、结构解析、exploded view、拆解               | `styles/exploded-view.md`          |
| 赛博朋克风科普插图风格 (Cyberpunk)              | 赛博朋克、cyberpunk、霓虹、未来科技                   | `styles/cyberpunk.md`              |
| 白板手绘风格科普插画风格 (Whiteboard)            | 白板、whiteboard、马克笔、手绘白板                   | `styles/whiteboard.md`             |
| 吉卜力风格科普插画 (Ghibli)                   | 吉卜力、宫崎骏、ghibli、miyazaki、龙猫               | `styles/ghibli.md`                 |
| 可爱卡哇伊贴纸风 (Kawaii Sticker)            | 卡哇伊、kawaii、贴纸、sticker、可爱                 | `styles/kawaii-sticker.md`         |
| 人物角色设定图 (Character Design Sheet)     | 角色设定、设定图、character design、设定稿            | `styles/character-design-sheet.md` |
| 撕纸分层特效 (Torn Paper Effect)           | 撕纸、分层特效、torn paper、纸层                    | `styles/torn-paper.md`             |
| 柔和简洁信息图表风格 (Soft Infographic)        | 柔和、简洁、信息图表、soft infographic、信息架构         | `styles/soft-infographic.md`       |
| 小清新风格插画模板 (Fresh Minimalist)         | 小清新、清新、fresh、扁平插画、治愈系                    | `styles/fresh-minimalist.md`       |
| 卡通流程图风格模板 (Cartoon Flowchart)        | 卡通流程图、3D卡通、floating island、游戏关卡          | `styles/cartoon-flowchart.md`      |
| 城市窗外风景照 (City Window View)           | 城市窗外、窗边风景、window view、室内外                | `styles/city-window-view.md`       |
| 日系黑白少年漫 (Shounen Manga)              | 少年漫、黑白漫画、shounen、manga、分镜                | `styles/shounen-manga.md`          |
| 街景 AR 标注图 (AR Annotation)            | AR标注、街景标注、ar annotation、导览图              | `styles/ar-annotation.md`          |
| 日系人物九宫格大头贴 (Photo Booth Strip)       | 九宫格、大头贴、purikura、photo booth             | `styles/photo-booth-strip.md`      |
| 电影主题复古邮票 (Vintage Stamp)             | 复古邮票、vintage stamp、邮票、postal             | `styles/vintage-stamp.md`          |
| 经典电影生成 PS1 游戏盒 (PS1 Game Case)       | PS1、游戏盒、playstation、game case、retro game | `styles/ps1-game-case.md`          |
| 珐琅徽章风格物品图 (Enamel Pin)               | 珐琅徽章、enamel pin、徽章、pin badge             | `styles/enamel-pin.md`             |
| 复古报纸风格 (Vintage Newspaper)           | 复古报纸、newspaper、报纸、newsprint              | `styles/vintage-newspaper.md`      |

> New styles are added by contributors. See [CONTRIBUTE.md](../CONTRIBUTE.md).

## Content Decomposition Guide

When filling in `MAIN CONTENT` after loading a style template:

1. **Identify the narrative arc**: progression (A→B→C), comparison (A vs B vs C), or expansion (center → branches)
2. **Name 3–5 milestones**: short, clear names (e.g., "Function Call", "MCP", "SKILL")
3. **Per-step content**:
   - **Label**: step name + one-sentence description
   - **Visual icons**: 1–3 symbols that represent it intuitively
   - **Action**: what happens at this stage conceptually
   - **Connection type**: follow the loaded style's arrow conventions

## Output Format

Output the complete prompt as a single code block — ready to paste into an image generator. Do not add explanation unless the user asks.

```
[Opening line]

=== SECTION ===
[content]

...

Quality: [quality tags]
```
