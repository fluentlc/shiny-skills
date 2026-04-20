# shiny-skills ✨

[中文](./README.zh.md)

A curated library of skills that make you go "wow" — each one transforms a mundane task into something surprisingly delightful.

## What is a Skill?

A **skill** is a SKILL.md file that an AI agent detects automatically. When a user's request matches the skill's trigger conditions, the agent loads the skill and follows its instructions — no plugins, no setup, just drop the folder into your skills directory.

## Skills

---

### 🎨 [shiny-image-creation-skill](./shiny-image-creation-skill/)

Transforms a one-line description into a fully structured AI image prompt. Supports 27+ visual styles — from Doraemon to Ghibli to Cyberpunk to PS1 Game Case.

**Input:**
```
Create an image showing the evolution from Function Call to MCP to SKILL, chalkboard style, 16:9
```

**Output:** A complete structured prompt ready to paste into Banana2, Midjourney, DALL-E, or Stable Diffusion.

**Style Gallery** (generated with Nano Banana Pro):

| | | | |
|---|---|---|---|
| ![doraemon](./shiny-image-creation-skill/gallery/doraemon.png) | ![doodle](./shiny-image-creation-skill/gallery/doodle.png) | ![chalkboard](./shiny-image-creation-skill/gallery/chalkboard.png) | ![chiikawa](./shiny-image-creation-skill/gallery/chiikawa.png) |
| Doraemon | Doodle | Chalkboard | Chiikawa |
| ![shinchan](./shiny-image-creation-skill/gallery/shinchan.png) | ![vintage-sketchnote](./shiny-image-creation-skill/gallery/vintage-sketchnote.png) | ![claymation](./shiny-image-creation-skill/gallery/claymation.png) | ![pop-art-xiaohongshu](./shiny-image-creation-skill/gallery/pop-art-xiaohongshu.png) |
| Shin-chan | Vintage Sketchnote | Claymation | Pop Art |
| ![superhero-comic](./shiny-image-creation-skill/gallery/superhero-comic.png) | ![anime-figurine](./shiny-image-creation-skill/gallery/anime-figurine.png) | ![exploded-view](./shiny-image-creation-skill/gallery/exploded-view.png) | ![cyberpunk](./shiny-image-creation-skill/gallery/cyberpunk.png) |
| Superhero Comic | Anime Figurine | Exploded View | Cyberpunk |
| ![whiteboard](./shiny-image-creation-skill/gallery/whiteboard.png) | ![ghibli](./shiny-image-creation-skill/gallery/ghibli.png) | ![kawaii-sticker](./shiny-image-creation-skill/gallery/kawaii-sticker.png) | ![character-design-sheet](./shiny-image-creation-skill/gallery/character-design-sheet.png) |
| Whiteboard | Ghibli | Kawaii Sticker | Character Design Sheet |
| ![torn-paper](./shiny-image-creation-skill/gallery/torn-paper.png) | ![soft-infographic](./shiny-image-creation-skill/gallery/soft-infographic.png) | ![fresh-minimalist](./shiny-image-creation-skill/gallery/fresh-minimalist.png) | ![cartoon-flowchart](./shiny-image-creation-skill/gallery/cartoon-flowchart.png) |
| Torn Paper | Soft Infographic | Fresh Minimalist | Cartoon Flowchart |
| ![city-window-view](./shiny-image-creation-skill/gallery/city-window-view.png) | ![shounen-manga](./shiny-image-creation-skill/gallery/shounen-manga.png) | ![ar-annotation](./shiny-image-creation-skill/gallery/ar-annotation.png) | ![photo-booth-strip](./shiny-image-creation-skill/gallery/photo-booth-strip.png) |
| City Window View | Shounen Manga | AR Annotation | Photo Booth Strip |
| ![vintage-stamp](./shiny-image-creation-skill/gallery/vintage-stamp.png) | ![ps1-game-case](./shiny-image-creation-skill/gallery/ps1-game-case.png) | ![enamel-pin](./shiny-image-creation-skill/gallery/enamel-pin.png) | |
| Vintage Stamp | PS1 Game Case | Enamel Pin | |

→ [Full documentation & installation](./shiny-image-creation-skill/)

---

> More skills coming. Contributions welcome.

## Installation

```bash
git clone https://github.com/fluentlc/shiny-skills.git

# Install a specific skill
cp -r shiny-skills/<skill-name> ~/.claude/skills/
```

Each skill directory contains its own README with usage details.

## Contributing

Want to add a new skill? Open a PR — any skill that makes someone's jaw drop is welcome.

## License

MIT
