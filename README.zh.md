# shiny-skills ✨

[English](./README.md)

一个精心策划的 Skill 库——每个 Skill 都能让人眼前一亮，把平淡无奇的任务变成令人惊喜的体验。

## 什么是 Skill？

**Skill** 是一个 SKILL.md 文件，AI Agent 会自动识别它。当用户的请求匹配到 Skill 的触发条件时，Agent 会加载该 Skill 并按其指引执行——无需插件、无需配置，只需将目录放入 Skills 目录即可。

## Skill 列表

---

### 🎨 [image-creation-prompt-skill](./image-creation-prompt-skill/)

将一句话描述转化为完整的结构化 AI 绘图 Prompt，支持 27+ 种视觉风格——从哆啦A梦到吉卜力，从赛博朋克到 PS1 游戏盒。

**输入：**
```
生成一张从Function Call到MCP到SKILL的发展历程图片，黑板报风格，16:9
```

**输出：** 一个完整的结构化 Prompt，直接粘贴到 Nano Banana、Midjourney、DALL-E 或 Stable Diffusion 即可使用。

**风格效果图**（由 Nano Banana Pro 生成）：

|                                                                                 |                                                                                     |                                                                                 |                                                                                             |
| ------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| ![doraemon](./image-creation-prompt-skill/gallery/doraemon.png)                 | ![doodle](./image-creation-prompt-skill/gallery/doodle.png)                         | ![chalkboard](./image-creation-prompt-skill/gallery/chalkboard.png)             | ![chiikawa](./image-creation-prompt-skill/gallery/chiikawa.png)                             |
| 哆啦A梦                                                                            | 手绘涂鸦                                                                                | 黑板报                                                                             | 吉伊卡哇                                                                                        |
| ![shinchan](./image-creation-prompt-skill/gallery/shinchan.png)                 | ![vintage-sketchnote](./image-creation-prompt-skill/gallery/vintage-sketchnote.png) | ![claymation](./image-creation-prompt-skill/gallery/claymation.png)             | ![pop-art-xiaohongshu](./image-creation-prompt-skill/gallery/pop-art-xiaohongshu.png)       |
| 蜡笔小新                                                                            | 复古怀旧                                                                                | 黏土定格                                                                            | 波普小红书                                                                                       |
| ![superhero-comic](./image-creation-prompt-skill/gallery/superhero-comic.png)   | ![anime-figurine](./image-creation-prompt-skill/gallery/anime-figurine.png)         | ![exploded-view](./image-creation-prompt-skill/gallery/exploded-view.png)       | ![cyberpunk](./image-creation-prompt-skill/gallery/cyberpunk.png)                           |
| 超级英雄漫画                                                                          | 动漫手办                                                                                | 爆炸视图                                                                            | 赛博朋克                                                                                        |
| ![whiteboard](./image-creation-prompt-skill/gallery/whiteboard.png)             | ![ghibli](./image-creation-prompt-skill/gallery/ghibli.png)                         | ![kawaii-sticker](./image-creation-prompt-skill/gallery/kawaii-sticker.png)     | ![character-design-sheet](./image-creation-prompt-skill/gallery/character-design-sheet.png) |
| 白板手绘                                                                            | 吉卜力                                                                                 | 卡哇伊贴纸                                                                           | 角色设定图                                                                                       |
| ![torn-paper](./image-creation-prompt-skill/gallery/torn-paper.png)             | ![soft-infographic](./image-creation-prompt-skill/gallery/soft-infographic.png)     | ![fresh-minimalist](./image-creation-prompt-skill/gallery/fresh-minimalist.png) | ![cartoon-flowchart](./image-creation-prompt-skill/gallery/cartoon-flowchart.png)           |
| 撕纸分层                                                                            | 柔和信息图                                                                               | 小清新                                                                             | 卡通流程图                                                                                       |
| ![city-window-view](./image-creation-prompt-skill/gallery/city-window-view.png) | ![shounen-manga](./image-creation-prompt-skill/gallery/shounen-manga.png)           | ![ar-annotation](./image-creation-prompt-skill/gallery/ar-annotation.png)       | ![photo-booth-strip](./image-creation-prompt-skill/gallery/photo-booth-strip.png)           |
| 城市窗外                                                                            | 少年漫                                                                                 | AR标注                                                                            | 九宫格大头贴                                                                                      |
| ![vintage-stamp](./image-creation-prompt-skill/gallery/vintage-stamp.png)       | ![ps1-game-case](./image-creation-prompt-skill/gallery/ps1-game-case.png)           | ![enamel-pin](./image-creation-prompt-skill/gallery/enamel-pin.png)             | ![vintage-newspaper](./image-creation-prompt-skill/gallery/vintage-newspaper.png)           |
| 复古邮票                                                                            | PS1游戏盒                                                                              | 珐琅徽章                                                                            | Vintage Newspaper                                                                           |

→ [完整文档与安装说明](./image-creation-prompt-skill/)

---

> 持续新增中，欢迎贡献。

## 安装

```bash
git clone https://github.com/fluentlc/shiny-skills.git

# 安装某个 Skill
cp -r shiny-skills/<skill-name> ~/.claude/skills/
```

每个 Skill 目录内都有独立的 README，包含详细的使用说明。

## 贡献

想添加新的 Skill？欢迎提 PR——任何能让人眼前一亮的 Skill 都欢迎加入。

## License

MIT
