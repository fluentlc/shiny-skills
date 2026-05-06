# shiny-skills ✨

[中文](./README.zh.md)

A curated library of skills that make you go "wow" — each one transforms a mundane task into something surprisingly delightful.

## What is a Skill?

A **skill** is a SKILL.md file that an AI agent detects automatically. When a user's request matches the skill's trigger conditions, the agent loads the skill and follows its instructions — no plugins, no setup, just drop the folder into your skills directory.

## Skills

---

### 🎨 [image-creation-prompt-skill](./image-creation-prompt-skill/)

Transforms a one-line description into a fully structured AI image prompt. Supports 27+ visual styles — from Doraemon to Ghibli to Cyberpunk to PS1 Game Case.

**Input:**
```
Create an image showing the evolution from Function Call to MCP to SKILL, chalkboard style, 16:9
```

**Output:** A complete structured prompt ready to paste into Nano Banana, Midjourney, DALL-E, or Stable Diffusion.

**Style Gallery** (generated with Nano Banana Pro):

|                                                                                 |                                                                                     |                                                                                 |                                                                                             |
| ------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| ![doraemon](./image-creation-prompt-skill/gallery/doraemon.png)                 | ![doodle](./image-creation-prompt-skill/gallery/doodle.png)                         | ![chalkboard](./image-creation-prompt-skill/gallery/chalkboard.png)             | ![chiikawa](./image-creation-prompt-skill/gallery/chiikawa.png)                             |
| Doraemon                                                                        | Doodle                                                                              | Chalkboard                                                                      | Chiikawa                                                                                    |
| ![shinchan](./image-creation-prompt-skill/gallery/shinchan.png)                 | ![vintage-sketchnote](./image-creation-prompt-skill/gallery/vintage-sketchnote.png) | ![claymation](./image-creation-prompt-skill/gallery/claymation.png)             | ![pop-art-xiaohongshu](./image-creation-prompt-skill/gallery/pop-art-xiaohongshu.png)       |
| Shin-chan                                                                       | Vintage Sketchnote                                                                  | Claymation                                                                      | Pop Art                                                                                     |
| ![superhero-comic](./image-creation-prompt-skill/gallery/superhero-comic.png)   | ![anime-figurine](./image-creation-prompt-skill/gallery/anime-figurine.png)         | ![exploded-view](./image-creation-prompt-skill/gallery/exploded-view.png)       | ![cyberpunk](./image-creation-prompt-skill/gallery/cyberpunk.png)                           |
| Superhero Comic                                                                 | Anime Figurine                                                                      | Exploded View                                                                   | Cyberpunk                                                                                   |
| ![whiteboard](./image-creation-prompt-skill/gallery/whiteboard.png)             | ![ghibli](./image-creation-prompt-skill/gallery/ghibli.png)                         | ![kawaii-sticker](./image-creation-prompt-skill/gallery/kawaii-sticker.png)     | ![character-design-sheet](./image-creation-prompt-skill/gallery/character-design-sheet.png) |
| Whiteboard                                                                      | Ghibli                                                                              | Kawaii Sticker                                                                  | Character Design Sheet                                                                      |
| ![torn-paper](./image-creation-prompt-skill/gallery/torn-paper.png)             | ![soft-infographic](./image-creation-prompt-skill/gallery/soft-infographic.png)     | ![fresh-minimalist](./image-creation-prompt-skill/gallery/fresh-minimalist.png) | ![cartoon-flowchart](./image-creation-prompt-skill/gallery/cartoon-flowchart.png)           |
| Torn Paper                                                                      | Soft Infographic                                                                    | Fresh Minimalist                                                                | Cartoon Flowchart                                                                           |
| ![city-window-view](./image-creation-prompt-skill/gallery/city-window-view.png) | ![shounen-manga](./image-creation-prompt-skill/gallery/shounen-manga.png)           | ![ar-annotation](./image-creation-prompt-skill/gallery/ar-annotation.png)       | ![photo-booth-strip](./image-creation-prompt-skill/gallery/photo-booth-strip.png)           |
| City Window View                                                                | Shounen Manga                                                                       | AR Annotation                                                                   | Photo Booth Strip                                                                           |
| ![vintage-stamp](./image-creation-prompt-skill/gallery/vintage-stamp.png)       | ![ps1-game-case](./image-creation-prompt-skill/gallery/ps1-game-case.png)           | ![enamel-pin](./image-creation-prompt-skill/gallery/enamel-pin.png)             | ![vintage-newspaper](./image-creation-prompt-skill/gallery/vintage-newspaper.png)           |
| Vintage Stamp                                                                   | PS1 Game Case                                                                       | Enamel Pin                                                                      | Vintage Newspaper                                                                           |
| ![black-white-educational-comic](./image-creation-prompt-skill/gallery/black-white-educational-comic.png) | ![handwritten-math-notes](./image-creation-prompt-skill/gallery/handwritten-math-notes.png) | ![urban-collage-poster](./image-creation-prompt-skill/gallery/urban-collage-poster.png) | ![luxury-event-poster](./image-creation-prompt-skill/gallery/luxury-event-poster.png)       |
| Black & White Educational Comic                                                 | Handwritten Math Notes                                                              | Urban Collage Poster                                                            | Luxury Event Poster                                                                         |
| ![chinese-ink-landscape](./image-creation-prompt-skill/gallery/chinese-ink-landscape.png) | ![3d-cartoon-figure](./image-creation-prompt-skill/gallery/3d-cartoon-figure.png) | ![3d-cartoon-blind-box](./image-creation-prompt-skill/gallery/3d-cartoon-blind-box.png) | ![futuristic-neon-poster](./image-creation-prompt-skill/gallery/futuristic-neon-poster.png) |
| Chinese Ink Landscape                                                           | 3D Cartoon Figure                                                                   | 3D Blind Box                                                                    | Futuristic Neon Poster                                                                      |
| ![cyberpunk-particle-stream](./image-creation-prompt-skill/gallery/cyberpunk-particle-stream.png) |                                                                                     |                                                                                 |                                                                                             |
| Cyberpunk Particle Stream                                                       |                                                                                     |                                                                                 |                                                                                             |

→ [Full documentation & installation](./image-creation-prompt-skill/)

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
