---
name: image-to-prompt-skill
description: Use when user uploads an image and wants to generate a structured prompt template and concrete prompt case from it. Triggers on image uploads with requests like "根据这张图生成 prompt", "reverse engineer this image", "分析这张图片的风格", or keywords like "image to prompt", "prompt template".
---

# Image to Prompt Skill

## Overview

Reverse-engineers uploaded images into two artifacts:

1. **Prompt Template** — A reusable structured prompt with `[PLACEHOLDER]` variables for generating similar images with different subjects.
2. **Prompt Case** — The concrete prompt with placeholders filled using actual content observed in the input image.

This skill is the reverse counterpart of `image-creation-prompt-skill`:
- `image-creation-prompt-skill` = forward: text description -> structured prompt
- `image-to-prompt-skill` = reverse: image -> structured prompt + reusable template

## Trigger Conditions

Activate when:
- User uploads an image (base64, file path, or URL) and asks for prompt generation
- Explicit requests: "根据这张图生成 prompt", "reverse engineer this image", "分析这张图片的风格", "拆解这张图的结构"
- Keywords: "image to prompt", "图片转 prompt", "prompt 模板", "逆向图片", "根据图片生成 prompt"

## 10-Step Visual Analysis Framework

Before generating output, systematically analyze the image across these 10 dimensions:

| Step | Dimension | What to Extract |
|------|-----------|-----------------|
| 1 | **Overall Style** | Art movement, visual genre, aesthetic label (e.g., "graffiti collage poster", "minimalist flat illustration") |
| 2 | **Color Scheme** | Primary/secondary/accent colors, contrast level, saturation, palette type (monochrome, complementary, analogous, triadic) |
| 3 | **Main Subject** | Central figure/object: identity, pose, expression, clothing, accessories, physical traits, proportions relative to frame |
| 4 | **Background Design** | Environment, depth of field, background elements, layering, spatial relationship to subject |
| 5 | **Text & Typography** | All visible text content, font styles, sizes, orientations, languages, placement strategy, hierarchy |
| 6 | **Composition & Perspective** | Framing, rule of thirds, symmetry/asymmetry, diagonal lines, camera angle, focal point, visual hierarchy |
| 7 | **Material & Texture** | Surface qualities: paper, metal, fabric, digital smoothness, brush strokes, torn edges, grain, gloss/matte |
| 8 | **Lighting & Mood** | Light direction, intensity, shadows, highlights, emotional tone, atmosphere, time of day feel |
| 9 | **Decorative & Auxiliary Elements** | Icons, borders, geometric shapes, patterns, filters, overlays, vignettes, watermarks, corner decorations |
| 10 | **Quality & Technical Parameters** | Estimated aspect ratio, resolution cues, suspected AI model parameters (e.g., `--ar 9:16 --v 5 --style raw`) |

## Output Format

Produce two code blocks in a single response.

### Block 1: Prompt Template

```
=== Overall Style ===
<[STYLE_NAME] art style — style description with [ART_STYLE], [ERA], [GENRE] placeholders>

=== Color Scheme ===
<Color palette description with [PRIMARY_COLOR], [SECONDARY_COLOR], [ACCENT_COLOR] placeholders>

=== Main Subject ===
<Subject template with [SUBJECT_NAME], [AGE], [GENDER], [POSE], [EXPRESSION], [CLOTHING], [ACCESSORIES] placeholders>

=== Background Design ===
<Background template with [SETTING], [DEPTH_OF_FIELD], [BG_ELEMENTS] placeholders>

=== Text & Typography ===
<Text template with [HEADLINE], [BODY_TEXT], [FONT_STYLE], [TEXT_PLACEMENT] placeholders>

=== Composition & Perspective ===
<Composition template with [FRAMING], [PERSPECTIVE], [FOCAL_POINT], [VISUAL_WEIGHT] placeholders>

=== Material & Texture ===
<Material template with [SURFACE_TYPE], [TEXTURE_DETAIL], [FINISH] placeholders>

=== Lighting & Mood ===
<Lighting template with [LIGHT_DIRECTION], [LIGHT_QUALITY], [MOOD], [ATMOSPHERE] placeholders>

=== Decorative & Auxiliary Elements ===
<Decorative template with [DECOR_TYPE], [PATTERN], [OVERLAY] placeholders>

=== Quality & Technical Parameters ===
<Quality tags with [ASPECT_RATIO], [MODEL_VERSION], [STYLE_PARAM], [QUALITY_TAGS] placeholders>
```

### Block 2: Prompt Case

Same 10 sections, but all placeholders are replaced with actual values observed in the input image. The case should read as a single coherent prompt that could be pasted directly into an image generator.

## Placeholder Naming Convention

- All caps, snake_case, wrapped in square brackets: `[SUBJECT_NAME]`, `[PRIMARY_COLOR]`
- Semantic naming: the placeholder name must describe what it represents
- Language-agnostic: placeholders use English for universal readability since the skill is open-source
- Predefined common placeholders (use these when applicable; invent new ones only when necessary):
  - `[STYLE_NAME]`
  - `[SUBJECT_NAME]` / `[SUBJECT_TYPE]` / `[SUBJECT_DESCRIPTION]`
  - `[AGE]` / `[GENDER]` / `[POSE]` / `[EXPRESSION]` / `[FACIAL_FEATURES]`
  - `[CLOTHING]` / `[ACCESSORIES]` / `[HAIR_STYLE]` / `[BODY_TYPE]`
  - `[PRIMARY_COLOR]` / `[SECONDARY_COLOR]` / `[ACCENT_COLOR]` / `[BACKGROUND_COLOR]`
  - `[SETTING]` / `[BG_ELEMENTS]` / `[DEPTH_OF_FIELD]` / `[ENVIRONMENT]`
  - `[HEADLINE]` / `[BODY_TEXT]` / `[FONT_STYLE]` / `[TEXT_PLACEMENT]` / `[LANGUAGE]`
  - `[FRAMING]` / `[PERSPECTIVE]` / `[FOCAL_POINT]` / `[VISUAL_WEIGHT]` / `[CAMERA_ANGLE]`
  - `[SURFACE_TYPE]` / `[TEXTURE_DETAIL]` / `[FINISH]` / `[MATERIAL]`
  - `[LIGHT_DIRECTION]` / `[LIGHT_QUALITY]` / `[LIGHT_COLOR]` / `[MOOD]` / `[ATMOSPHERE]`
  - `[DECOR_TYPE]` / `[PATTERN]` / `[OVERLAY]` / `[BORDER_STYLE]`
  - `[ASPECT_RATIO]` / `[MODEL_VERSION]` / `[STYLE_PARAM]` / `[QUALITY_TAGS]` / `[RESOLUTION]`
  - `[ART_STYLE]` / `[ERA]` / `[GENRE]`

## Content Quality Rules

1. **Be specific, not vague.** Instead of "modern design," write "asymmetrical layout with strong diagonal lines and overlapping geometric shapes."
2. **Preserve proportions and relationships.** If the subject occupies 30% of the frame and is positioned left-of-center, say so.
3. **Distinguish observed from inferred.** Observed: "black and orange color scheme." Inferred: "likely generated with --v 5 --style raw."
4. **Template must be truly reusable.** A user should be able to swap `[SUBJECT_NAME]` and `[SUBJECT_TYPE]` and get a coherent new prompt for a different subject in the same style.
5. **Quality tags go last.** Always end with technical/quality parameters so they can be easily copied to image generators.
6. **Use the 10 sections consistently.** Every output must have all 10 sections. If a section has minimal content (e.g., no text in a pure photograph), explicitly state "No text elements present" rather than omitting the section.

## Few-Shot Learning

Before generating, review examples in `examples/` to understand expected analysis depth and output quality. Each example demonstrates the 10-step framework applied to a real image.

### Example Reference Files

| Example | Style | Key Learning |
|---------|-------|--------------|
| `examples/urban-collage-poster-example.md` | Graffiti collage poster | Complex multi-layer composition with text, portrait, and urban elements |
| `examples/neon-cyberpunk-poster-example.md` | Cyberpunk neon poster | High-contrast futuristic style with glow effects and atmospheric lighting |
| `examples/portrait-photography-example.md` | Studio portrait photography | Natural subject with minimal graphic elements, emphasis on lighting and pose |
