# image-to-prompt-skill

[中文](./README.zh.md)

A Claude Skill that reverse-engineers uploaded images into structured prompt templates and concrete prompt cases.

## What It Does

Upload any image and get two artifacts:

1. **Prompt Template** — A reusable structured prompt with `[PLACEHOLDER]` variables. Save it and adapt for generating similar images with different subjects.
2. **Prompt Case** — The concrete prompt with placeholders filled using actual content from the input image. Paste directly into an image generator.

**Input:**
Upload an image and say:
```
Generate a prompt template from this image
```

**Output:**
```
=== Overall Style ===
...

=== Color Scheme ===
...

(10 sections of complete Prompt Template + Prompt Case)
```

## Relationship to image-creation-prompt-skill

- `image-creation-prompt-skill` = Forward: text description -> structured prompt
- `image-to-prompt-skill` = Reverse: image -> structured prompt + reusable template

Both share the same output format convention for seamless user experience.

## Installation

This Skill relies on the Agent's file reading capability (Claude Code / OpenClaw or equivalent). Copy the entire Skill directory, not just `SKILL.md`.

```bash
# Clone the repo
git clone https://github.com/fluentlc/shiny-skills.git

# Copy the skill directory to Claude Code skills folder
cp -r shiny-skills/image-to-prompt-skill ~/.claude/skills/
```

## Usage

After installation, upload any image and describe your request:

```
Generate a prompt template from this image
Analyze the style of this image
Reverse engineer this image
```

Claude will automatically recognize the Skill, perform a 10-step visual analysis, and output both the Prompt Template and Case.

## 10-Step Visual Analysis Framework

| Step | Dimension | Analysis Content |
|------|-----------|-----------------|
| 1 | **Overall Style** | Art movement, visual genre, aesthetic label |
| 2 | **Color Scheme** | Primary/secondary/accent colors, contrast, saturation |
| 3 | **Main Subject** | Central figure/object: features, pose, expression, clothing |
| 4 | **Background Design** | Environment, depth of field, elements, spatial relationship |
| 5 | **Text & Typography** | Visible text, fonts, sizes, orientations, hierarchy |
| 6 | **Composition & Perspective** | Framing, symmetry, lines, camera angle, focal point |
| 7 | **Material & Texture** | Surface qualities: paper, metal, fabric, digital smoothness |
| 8 | **Lighting & Mood** | Light direction, intensity, shadows, emotional tone |
| 9 | **Decorative Elements** | Icons, borders, shapes, patterns, filters, overlays |
| 10 | **Quality & Technical** | Estimated aspect ratio, resolution, model parameters |

## Placeholder Naming Convention

Template placeholders use English ALL_CAPS_SNAKE_CASE for universal readability:

- `[SUBJECT_NAME]` — Subject name
- `[PRIMARY_COLOR]` — Primary color
- `[POSE]` — Subject pose
- `[CLOTHING]` — Clothing description
- `[BACKGROUND_COLOR]` — Background color
- `[ASPECT_RATIO]` — Aspect ratio
- ... (full list in SKILL.md)

## Examples

See [`examples/`](./examples/) for real-world case studies:

| Example | Style | Highlights |
|---------|-------|------------|
| [urban-collage-poster](./examples/urban-collage-poster-example.md) | Graffiti collage poster | Multi-layer text, portrait cutout, urban elements |

## Request New Examples

Found an interesting visual style you'd like documented? Open an Issue with the image attached, and contributors will generate a complete Prompt Template and Case for it.

## Contribute

See [`CONTRIBUTE.md`](./CONTRIBUTE.md).

## License

MIT
