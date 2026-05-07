# image-to-prompt Skill Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create a new Claude Skill (`image-to-prompt-skill/`) that reverse-engineers uploaded images into reusable prompt templates and concrete prompt cases, positioned as a sibling to the existing `image-creation-prompt-skill/`.

**Architecture:** Pure documentation skill with no code dependencies. Core is `SKILL.md` containing trigger conditions, a 10-step visual analysis framework, output format spec, and placeholder naming convention. Few-shot examples in `examples/` teach the Agent expected analysis depth. Root READMEs updated to list the new skill.

**Tech Stack:** Markdown files only. No build, no tests, no dependencies.

---

## File Structure

```
image-to-prompt-skill/
├── SKILL.md                                    # Core skill definition
├── README.md                                   # English usage docs
├── README.zh.md                                # Chinese usage docs
├── examples/
│   ├── urban-collage-poster-example.md         # Few-shot: graffiti collage poster
│   ├── neon-cyberpunk-poster-example.md        # Few-shot: cyberpunk neon poster
│   └── portrait-photography-example.md         # Few-shot: studio portrait
├── CONTRIBUTE.md
└── CONTRIBUTE.zh.md

README.md (root)                                # Add skill listing
README.zh.md (root)                             # Add skill listing
```

---

### Task 1: Create SKILL.md

**Files:**
- Create: `image-to-prompt-skill/SKILL.md`

- [ ] **Step 1: Write SKILL.md**

```markdown
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
=== [Style Name] ===
[Style description with placeholders for adaptable elements]

=== Color Scheme ===
[Color palette description with [PRIMARY_COLOR], [SECONDARY_COLOR], [ACCENT_COLOR] placeholders]

=== Main Subject ===
[Subject template with [SUBJECT_NAME], [AGE], [GENDER], [POSE], [EXPRESSION], [CLOTHING], [ACCESSORIES] placeholders]

=== Background Design ===
[Background template with [SETTING], [DEPTH_OF_FIELD], [BG_ELEMENTS] placeholders]

=== Text & Typography ===
[Text template with [HEADLINE], [BODY_TEXT], [FONT_STYLE], [TEXT_PLACEMENT] placeholders]

=== Composition & Perspective ===
[Composition template with [FRAMING], [PERSPECTIVE], [FOCAL_POINT], [VISUAL_WEIGHT] placeholders]

=== Material & Texture ===
[Material template with [SURFACE_TYPE], [TEXTURE_DETAIL], [FINISH] placeholders]

=== Lighting & Mood ===
[Lighting template with [LIGHT_DIRECTION], [LIGHT_QUALITY], [MOOD], [ATMOSPHERE] placeholders]

=== Decorative Elements ===
[Decorative template with [DECOR_TYPE], [PATTERN], [OVERLAY] placeholders]

=== Quality & Technical ===
[Quality tags with [ASPECT_RATIO], [MODEL_VERSION], [STYLE_PARAM], [QUALITY_TAGS] placeholders]
```

### Block 2: Prompt Case

Same 10 sections, but all placeholders are replaced with actual values observed in the input image. The case should read as a single coherent prompt that could be pasted directly into an image generator.

## Placeholder Naming Convention

- All caps, snake_case, wrapped in square brackets: `[SUBJECT_NAME]`, `[PRIMARY_COLOR]`
- Semantic naming: the placeholder name must describe what it represents
- Language-agnostic: placeholders use English for universal readability since the skill is open-source
- Predefined common placeholders (use these when applicable; invent new ones only when necessary):
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
| `examples/urban-collage-poster-example.md` | Graffiti collage poster | Complex multi-layer composition with text, portrait cutout, and urban elements |
| `examples/neon-cyberpunk-poster-example.md` | Cyberpunk neon poster | High-contrast futuristic style with glow effects and atmospheric lighting |
| `examples/portrait-photography-example.md` | Studio portrait photography | Natural subject with minimal graphic elements, emphasis on lighting and pose |
```

- [ ] **Step 2: Verify placeholder naming consistency**

Run:
```bash
grep -oE '\[[A-Z_]+\]' image-to-prompt-skill/SKILL.md | sort -u
```
Expected: All placeholders match `[ALL_CAPS_SNAKE_CASE]` pattern. No lowercase or camelCase placeholders.

- [ ] **Step 3: Verify all 10 sections are declared**

Run:
```bash
grep -c '^=== .* ===$' image-to-prompt-skill/SKILL.md
```
Expected: Count >= 10 (the template block has 10 sections).

- [ ] **Step 4: Commit**

```bash
git add image-to-prompt-skill/SKILL.md
git commit -m "feat: add image-to-prompt SKILL.md with 10-step analysis framework

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>"
```

---

### Task 2: Create Urban Collage Poster Example

**Files:**
- Create: `image-to-prompt-skill/examples/urban-collage-poster-example.md`

- [ ] **Step 1: Write example file**

```markdown
# Example: Urban Graffiti Collage Poster

## User Input

[Image: A black and orange graffiti-style collage poster featuring a female professional portrait]

User request: "根据这张图片生成 prompt 模板和案例"

## Generated Prompt Template

```
=== [ART_STYLE] ===
Graffiti collage poster style, high-contrast [PRIMARY_COLOR] and [SECONDARY_COLOR] color scheme, urban street art aesthetic, layered text elements with bold [LANGUAGE] typography, mixed-media composition, dynamic layout with overlapping geometric shapes and torn paper textures, photorealistic portrait cutout integrated into abstract background, modern graphic design influence, [RESOLUTION], masterpiece detail.

=== Color Scheme ===
[PRIMARY_COLOR] and [SECONDARY_COLOR] high-contrast palette, [SATURATION_LEVEL] saturation, [CONTRAST_LEVEL] contrast, [COLOR_HARMONY_TYPE] color harmony with [ACCENT_COLOR] accents.

=== Main Subject ===
[SUBJECT_NAME], [AGE] years old, [ZODIAC_SIGN], [EXPRESSION] [GENDER] professional in a [CLOTHING], [HAIR_STYLE], wearing [ACCESSORIES], standing in [POSE], monochrome portrait with [OUTLINE_STYLE], positioned [POSITION] against vibrant background.

=== Background Design ===
Urban cityscape collage featuring [BG_ELEMENTS_1], [BG_ELEMENTS_2], [BG_ELEMENTS_3], and [BG_ELEMENTS_4], interwoven with large-scale [LANGUAGE] characters in bold [FONT_COLOR] font on [BLOCK_COLOR] blocks, creating a visually dense and energetic environment.

=== Text & Typography ===
[INTERESTS], [CURRENT_READING], [QUOTE_TEXT], [LABEL_TEXT], [ENGLISH_QUOTE], all styled in various fonts and orientations, placed strategically across the image to balance visual hierarchy and narrative flow.

=== Composition & Perspective ===
[COMPOSITION_TYPE] layout with [LINE_TYPE], [IMPACT_LEVEL] visual impact, sense of [MOVEMENT_TYPE] and [ENERGY_TYPE], [THEME_CONTRAST] meets [THEME_CONTRAST_2], [TONE] tone with a touch of [CREATIVE_TOUCH].

=== Material & Texture ===
[SURFACE_TYPE] surface with [TEXTURE_1] textures, [TEXTURE_2] edges, [TEXTURE_3] portrait treatment, [FINISH] finish creating [DEPTH_EFFECT].

=== Lighting & Mood ===
[LIGHT_QUALITY] lighting with [CONTRAST_TYPE] contrast, [SHADOW_STYLE] shadows, [HIGHLIGHT_STYLE] highlights, [MOOD] atmosphere with [EMOTIONAL_QUALITY] undertones.

=== Decorative Elements ===
[DECOR_1] geometric shapes, [DECOR_2] patterns, [DECOR_3] overlays, [DECOR_4] corners, adding visual complexity and urban authenticity.

=== Quality & Technical ===
ultra-detailed, sharp focus, cinematic lighting, high contrast, digital illustration, AI-generated artwork, --ar [ASPECT_RATIO] --v [MODEL_VERSION] --style [STYLE_PARAM]
```

## Generated Prompt Case

```
=== Graffiti Collage Poster Style ===
Graffiti collage poster style, high-contrast black and orange color scheme, urban street art aesthetic, layered text elements with bold Chinese typography, mixed-media composition, dynamic layout with overlapping geometric shapes and torn paper textures, photorealistic portrait cutout integrated into abstract background, modern graphic design influence, 8k resolution, masterpiece detail.

=== Color Scheme ===
Black and orange high-contrast palette, high saturation, extreme contrast, complementary color harmony with white accent outlines.

=== Main Subject ===
Employee Name, 25 years old, Capricorn, smiling female professional in a dark blazer, short hair, wearing earrings, standing in profile pose, monochrome portrait with white outline, positioned centrally against vibrant background.

=== Background Design ===
Urban cityscape collage featuring graffiti-covered walls, power lines, billboards, and fragmented architectural elements, interwoven with large-scale Chinese characters in bold black font on orange blocks, creating a visually dense and energetic environment.

=== Text & Typography ===
Interests: movies, reading, poster design, Currently reading: Data Analysis, Growth Hacker, A designer who can't do data analysis is not a good operator, Employee Name Label, A DESIGNER WHO CAN'T DO DATA ANALYSIS IS NOT A GOOD OPERATOR, all styled in various fonts and orientations, placed strategically across the image to balance visual hierarchy and narrative flow.

=== Composition & Atmosphere ===
Asymmetrical layout with strong diagonal lines, high visual impact, sense of movement and energy, modern corporate culture meets street art rebellion, welcoming tone with a touch of edgy creativity.

=== Material & Texture ===
Mixed-media surface with torn paper textures, rough-cut edges, monochrome portrait treatment with white outline, matte and glossy contrast finish creating depth and visual interest.

=== Lighting & Mood ===
High-contrast lighting with dramatic contrast, hard shadows, bright highlights on orange elements, energetic atmosphere with rebellious creative undertones.

=== Decorative Elements ===
Overlapping geometric shapes, urban graffiti patterns, abstract paint splatter overlays, torn paper corner effects, adding visual complexity and urban authenticity.

=== Quality & Technical ===
ultra-detailed, sharp focus, cinematic lighting, high contrast, digital illustration, AI-generated artwork, --ar 9:16 --v 5 --style raw
```
```

- [ ] **Step 2: Verify placeholder naming**

Run:
```bash
grep -oE '\[[A-Z_]+\]' image-to-prompt-skill/examples/urban-collage-poster-example.md | sort -u
```
Expected: All uppercase snake_case. No violations.

- [ ] **Step 3: Verify 10 sections in both template and case**

Run:
```bash
grep -c '^=== .* ===$' image-to-prompt-skill/examples/urban-collage-poster-example.md
```
Expected: Count = 20 (10 in template + 10 in case).

- [ ] **Step 4: Commit**

```bash
git add image-to-prompt-skill/examples/urban-collage-poster-example.md
git commit -m "feat: add urban collage poster example with template and case

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>"
```

---

### Task 3: Create Neon Cyberpunk Poster Example

**Files:**
- Create: `image-to-prompt-skill/examples/neon-cyberpunk-poster-example.md`

- [ ] **Step 1: Write example file**

```markdown
# Example: Neon Cyberpunk Poster

## User Input

[Image: A futuristic cyberpunk poster with neon glow effects on dark background]

User request: "根据这张图片生成 prompt 模板和案例"

## Generated Prompt Template

```
=== [ART_STYLE] ===
[GENRE] poster style, [LIGHTING_TYPE] lighting effects, [COLOR_TEMPERATURE] color temperature, futuristic [ERA] aesthetic, [EFFECT_TYPE] glow effects, [STYLE_DESCRIPTOR] composition, [ATMOSPHERE_TYPE] atmosphere, [RESOLUTION], [QUALITY_DESCRIPTOR].

=== Color Scheme ===
[PRIMARY_COLOR] and [SECONDARY_COLOR] neon palette on [BACKGROUND_COLOR] background, [ACCENT_COLOR] accent highlights, [SATURATION_LEVEL] saturation, [CONTRAST_LEVEL] contrast with [EFFECT_TYPE] bloom.

=== Main Subject ===
[SUBJECT_NAME], [SUBJECT_TYPE], [EXPRESSION] [GENDER] figure wearing [CLOTHING] with [ACCESSORIES], [POSE] pose, [LIGHTING_EFFECT] rim lighting, [COLOR_TEMPERATURE] skin tone under neon, [DETAIL_LEVEL] facial detail.

=== Background Design ===
[SETTING] cityscape with [BG_ELEMENTS_1], [BG_ELEMENTS_2], [BG_ELEMENTS_3], layered [DEPTH_EFFECT] depth, [ATMOSPHERE_TYPE] atmospheric haze, [REFLECTION_TYPE] wet surface reflections.

=== Text & Typography ===
[HEADLINE] in [FONT_STYLE] font with [EFFECT_TYPE] glow effect, [SUBHEADLINE] in [SECONDARY_FONT] style, [DECOR_TEXT] as background texture, [PLACEMENT] placement creating [HIERARCHY_TYPE] hierarchy.

=== Composition & Perspective ===
[COMPOSITION_TYPE] framing with [SUBJECT_POSITION], [PERSPECTIVE_TYPE] perspective, [FOCAL_POINT] focal emphasis, [DEPTH_EFFECT] depth layers, [VISUAL_FLOW] visual flow directing attention.

=== Material & Texture ===
[SURFACE_TYPE] surfaces with [TEXTURE_1] reflections, [TEXTURE_2] metallic sheen, [TEXTURE_3] digital grain, [FINISH] material finish on clothing and environment.

=== Lighting & Mood ===
[LIGHT_DIRECTION] neon lighting from [LIGHT_SOURCES], [LIGHT_QUALITY] light quality with [SHADOW_STYLE] shadows, [HIGHLIGHT_STYLE] specular highlights, [MOOD] mood with [EMOTIONAL_QUALITY] tension.

=== Decorative Elements ===
[DECOR_1] circuit patterns, [DECOR_2] holographic overlays, [DECOR_3] scan lines, [DECOR_4] data streams, [DECOR_5] lens flares enhancing futuristic feel.

=== Quality & Technical ===
[QUALITY_TAGS], --ar [ASPECT_RATIO] --v [MODEL_VERSION] --style [STYLE_PARAM] --stylize [STYLIZE_VALUE]
```

## Generated Prompt Case

```
=== Neon Cyberpunk Poster Style ===
Cyberpunk neon poster style, vibrant neon lighting effects, cool blue-purple color temperature, futuristic dystopian aesthetic, chromatic aberration glow effects, cinematic composition, rain-soaked atmosphere, 8k resolution, masterpiece quality.

=== Color Scheme ===
Electric blue and magenta neon palette on deep black background, cyan accent highlights, ultra-high saturation, extreme contrast with chromatic aberration bloom and light leak effects.

=== Main Subject ===
Mysterious hacker, young adult, determined female figure wearing black tactical jacket with holographic visor, three-quarter pose facing left, electric blue rim lighting, pale skin tone under neon, hyper-detailed facial features with subtle cybernetic implants.

=== Background Design ===
Futuristic Tokyo cityscape with towering holographic billboards, rain-soaked streets, flying vehicles, layered atmospheric depth, dense fog and atmospheric haze, wet asphalt surface reflections mirroring neon signs.

=== Text & Typography ===
"NEON DREAMS" in bold sans-serif font with magenta glow effect, "2077" in thin monospace style, Japanese katakana characters as background texture, asymmetric placement creating dynamic visual hierarchy.

=== Composition & Perspective ===
Rule-of-thirds framing with subject positioned at left intersection, low-angle perspective looking up at skyline, strong focal emphasis on subject's face, three depth layers (subject, midground signs, distant towers), diagonal visual flow from lower left to upper right directing attention.

=== Material & Texture ===
Wet synthetic surfaces with mirror-like reflections, brushed metallic sheen on visor, subtle digital grain overlay, matte rubber material finish on tactical clothing and glossy wet concrete environment.

=== Lighting & Mood ===
Multi-directional neon lighting from signs above and street-level below, harsh artificial light quality with deep black shadows, intense specular highlights on wet surfaces, tense mood with mysterious anticipation and urban isolation.

=== Decorative Elements ===
Glowing circuit board patterns on jacket edges, translucent holographic data overlays floating in foreground, subtle horizontal scan lines across image, cascading binary data streams in background, hexagonal lens flares from bright light sources enhancing futuristic feel.

=== Quality & Technical ===
ultra-detailed, sharp focus, cinematic lighting, ray tracing reflections, volumetric fog, digital illustration, concept art, --ar 9:16 --v 6 --style raw --stylize 250
```
```

- [ ] **Step 2: Verify placeholder naming**

Run:
```bash
grep -oE '\[[A-Z_]+\]' image-to-prompt-skill/examples/neon-cyberpunk-poster-example.md | sort -u
```
Expected: All uppercase snake_case.

- [ ] **Step 3: Verify 10 sections in both template and case**

Run:
```bash
grep -c '^=== .* ===$' image-to-prompt-skill/examples/neon-cyberpunk-poster-example.md
```
Expected: Count = 20.

- [ ] **Step 4: Commit**

```bash
git add image-to-prompt-skill/examples/neon-cyberpunk-poster-example.md
git commit -m "feat: add neon cyberpunk poster example

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>"
```

---

### Task 4: Create Portrait Photography Example

**Files:**
- Create: `image-to-prompt-skill/examples/portrait-photography-example.md`

- [ ] **Step 1: Write example file**

```markdown
# Example: Studio Portrait Photography

## User Input

[Image: A professional studio headshot portrait of a business person]

User request: "根据这张图片生成 prompt 模板和案例"

## Generated Prompt Template

```
=== [ART_STYLE] ===
[PHOTOGRAPHY_TYPE] photography, [STYLE_DESCRIPTOR] style, [COLOR_GRADING] color grading, [ERA] aesthetic, [MOOD] mood, [RESOLUTION], [QUALITY_DESCRIPTOR].

=== Color Scheme ===
[PRIMARY_TONE] dominant tones with [SECONDARY_TONE] undertones, [SKIN_TONE] skin tone rendering, [BACKGROUND_COLOR] background, [SATURATION_LEVEL] saturation, [CONTRAST_LEVEL] contrast.

=== Main Subject ===
[SUBJECT_NAME], [AGE] years old, [GENDER], [EXPRESSION] expression, [POSE] pose, wearing [CLOTHING] with [ACCESSORIES], [HAIR_STYLE] hair, [FACIAL_FEATURES] facial features, [BODY_TYPE] build.

=== Background Design ===
[BACKGROUND_TYPE] background with [BG_DESCRIPTION], [DEPTH_OF_FIELD] depth of field, [BG_TONE] tone, seamless transition from subject to backdrop.

=== Text & Typography ===
No text elements present — pure photographic portrait without typography or graphic overlays.

=== Composition & Perspective ===
[FRAMING] framing with [HEADROOM] headroom, [EYE_LEVEL] eye-level perspective, [SUBJECT_POSITION] subject position, [CROP_TYPE] crop, [VISUAL_WEIGHT] visual weight balanced.

=== Material & Texture ===
[SKIN_TEXTURE] skin texture, [FABRIC_TEXTURE] fabric texture in clothing, [HAIR_TEXTURE] hair detail, [BACKGROUND_TEXTURE] background surface texture.

=== Lighting & Mood ===
[LIGHTING_PATTERN] lighting pattern with [LIGHT_DIRECTION] main light, [FILL_LIGHT] fill light, [SHADOW_SOFTNESS] shadow quality, [CATCHLIGHT] catchlights in eyes, [MOOD] mood with [EMOTIONAL_QUALITY] emotional quality.

=== Decorative Elements ===
[DECOR_1] subtle vignette, [DECOR_2] natural skin retouching, minimal decorative elements to maintain photographic authenticity.

=== Quality & Technical ===
[QUALITY_TAGS], shallow depth of field, [LENS_TYPE] lens characteristics, --ar [ASPECT_RATIO] --v [MODEL_VERSION] --style [STYLE_PARAM]
```

## Generated Prompt Case

```
=== Studio Portrait Photography Style ===
Professional studio portrait photography, clean corporate style, warm neutral color grading, contemporary aesthetic, approachable and confident mood, 8k resolution, masterpiece quality.

=== Color Scheme ===
Warm beige and soft brown dominant tones with subtle golden undertones, natural warm skin tone rendering, light gray seamless background, moderate saturation, medium contrast with gentle tonal gradation.

=== Main Subject ===
Senior Executive, 45 years old, male, warm confident smile expression, three-quarter turn pose facing slightly right, wearing navy blue tailored suit with white dress shirt and subtle patterned tie, short gray-streaked hair neatly styled, strong jawline with warm brown eyes, athletic build.

=== Background Design ===
Solid seamless background with light gray tone, shallow depth of field with subtle background blur, neutral cool tone, clean seamless transition from subject to backdrop with no visible edges or shadows.

=== Text & Typography ===
No text elements present — pure photographic portrait without typography or graphic overlays.

=== Composition & Perspective ===
Tight head-and-shoulders framing with moderate headroom, straight-on eye-level perspective, subject centered with slight rule-of-thirds bias placing eyes at upper third line, classic portrait crop at mid-torso, visual weight balanced with negative space on left side.

=== Material & Texture ===
Natural realistic skin texture with subtle pores and fine lines, smooth wool-blend fabric texture in suit jacket with visible weave pattern, well-groomed hair with individual strand detail, matte seamless paper background texture.

=== Lighting & Mood ===
Rembrandt lighting pattern with 45-degree main light from upper left, soft fill light from camera right reducing shadow density, soft-edged shadow quality with gradual falloff, distinct rectangular catchlights in both eyes, professional mood with trustworthy warmth and executive authority.

=== Decorative Elements ===
Subtle dark vignette at corners drawing focus to subject, natural skin retouching preserving texture while minimizing blemishes, minimal decorative elements to maintain photographic authenticity.

=== Quality & Technical ===
ultra-detailed, sharp focus on eyes, professional studio lighting, shallow depth of field, 85mm lens characteristics with natural perspective compression, --ar 4:5 --v 6 --style raw
```
```

- [ ] **Step 2: Verify placeholder naming**

Run:
```bash
grep -oE '\[[A-Z_]+\]' image-to-prompt-skill/examples/portrait-photography-example.md | sort -u
```
Expected: All uppercase snake_case.

- [ ] **Step 3: Verify 10 sections in both template and case**

Run:
```bash
grep -c '^=== .* ===$' image-to-prompt-skill/examples/portrait-photography-example.md
```
Expected: Count = 20.

- [ ] **Step 4: Commit**

```bash
git add image-to-prompt-skill/examples/portrait-photography-example.md
git commit -m "feat: add portrait photography example

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>"
```

---

### Task 5: Create README.zh.md

**Files:**
- Create: `image-to-prompt-skill/README.zh.md`

- [ ] **Step 1: Write README.zh.md**

```markdown
# image-to-prompt-skill

[English](./README.md)

一个将上传的图片逆向拆解为结构化 Prompt 模板和具体 Prompt 案例的 Skill。

## 功能

上传一张图片，自动生成两份产物：

1. **Prompt 模板** — 带 `[PLACEHOLDER]` 占位符的可复用模板，保存后可用于生成同风格的不同主题图片
2. **Prompt 案例** — 用当前图片实际内容填充的完整 Prompt，可直接粘贴到图像生成工具使用

**输入：**
上传一张图片，说：
```
根据这张图生成 prompt 模板
```

**输出：**
```
=== [Style Name] ===
...

=== Color Scheme ===
...

（共 10 个 Section 的完整 Prompt 模板 + Prompt 案例）
```

## 与 image-creation-prompt-skill 的关系

- `image-creation-prompt-skill` = 正向：一句话描述 -> 结构化 Prompt
- `image-to-prompt-skill` = 逆向：一张图片 -> 结构化 Prompt + 可复用模板

两者共享相同的输出格式规范，方便用户无缝切换。

## 安装

此 Skill 依赖 Agent 的文件读取能力（Claude Code / OpenClaw 或同等工具）。需要将整个 Skill 目录复制过去，而非仅 `SKILL.md` 单个文件。

```bash
# 克隆仓库
git clone https://github.com/fluentlc/shiny-skills.git

# 将 skill 目录复制到 Claude Code skills 文件夹
cp -r shiny-skills/image-to-prompt-skill ~/.claude/skills/
```

## 使用方法

安装后，上传任意图片并描述你的需求：

```
根据这张图生成 prompt 模板
分析这张图片的风格
拆解这张图的结构
```

Claude 会自动识别 Skill，对图片进行 10 步视觉分析，并输出 Prompt 模板和案例。

## 10 步视觉分析框架

| 步骤 | 维度 | 分析内容 |
|------|------|----------|
| 1 | 整体风格 | 艺术流派、视觉风格、美学标签 |
| 2 | 色彩方案 | 主色/辅色/强调色、对比度、饱和度 |
| 3 | 主体分析 | 人物/物品的核心特征、姿态、表情、服饰 |
| 4 | 背景设计 | 环境、景深、背景元素、空间关系 |
| 5 | 文字排版 | 可见文字内容、字体、大小、方向、层级 |
| 6 | 构图视角 | 取景、对称性、线条、视角、焦点 |
| 7 | 材质纹理 | 表面质感：纸张、金属、织物、数字平滑度 |
| 8 | 光影氛围 | 光源方向、强度、阴影、情绪基调 |
| 9 | 装饰元素 | 图标、边框、几何图形、图案、滤镜 |
| 10 | 技术参数 | 推测的宽高比、分辨率、模型参数 |

## 占位符命名规范

模板中的占位符使用英文大写下划线格式，便于全球用户复用：

- `[SUBJECT_NAME]` — 主体名称
- `[PRIMARY_COLOR]` — 主色调
- `[POSE]` — 姿态
- `[CLOTHING]` — 服饰
- `[BACKGROUND_COLOR]` — 背景色
- `[ASPECT_RATIO]` — 宽高比
- ...（完整列表见 SKILL.md）

## 案例

参见 [`examples/`](./examples/) 目录中的真实案例分析：

| 案例 | 风格 | 特点 |
|------|------|------|
| [urban-collage-poster](./examples/urban-collage-poster-example.md) | 涂鸦拼贴海报 | 多层文字、人像剪影、城市元素 |
| [neon-cyberpunk-poster](./examples/neon-cyberpunk-poster-example.md) | 赛博朋克霓虹海报 | 高对比霓虹光效、未来感氛围 |
| [portrait-photography](./examples/portrait-photography-example.md) | 人像摄影 | 自然主体、光影分析、无文字元素 |

## 请求新案例

遇到一种很好看的图片风格，想让它被收录为分析案例？提一个 Issue 并附上图片，贡献者会为你生成完整的 Prompt 模板和案例。

## 贡献

参见 [`CONTRIBUTE.zh.md`](./CONTRIBUTE.zh.md)。

## License

MIT
```

- [ ] **Step 2: Verify internal links**

Run:
```bash
grep -E '\[.*\]\(\./.*\)' image-to-prompt-skill/README.zh.md
```
Expected: Links point to `./README.md`, `./examples/`, `./CONTRIBUTE.zh.md`.

- [ ] **Step 3: Commit**

```bash
git add image-to-prompt-skill/README.zh.md
git commit -m "docs: add Chinese README for image-to-prompt skill

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>"
```

---

### Task 6: Create README.md

**Files:**
- Create: `image-to-prompt-skill/README.md`

- [ ] **Step 1: Write README.md**

```markdown
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
=== [Style Name] ===
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
| [neon-cyberpunk-poster](./examples/neon-cyberpunk-poster-example.md) | Cyberpunk neon poster | High-contrast glow effects, futuristic atmosphere |
| [portrait-photography](./examples/portrait-photography-example.md) | Studio portrait | Natural subject, lighting analysis, no text elements |

## Request New Examples

Found an interesting visual style you'd like documented? Open an Issue with the image attached, and contributors will generate a complete Prompt Template and Case for it.

## Contribute

See [`CONTRIBUTE.md`](./CONTRIBUTE.md).

## License

MIT
```

- [ ] **Step 2: Verify internal links**

Run:
```bash
grep -E '\[.*\]\(\./.*\)' image-to-prompt-skill/README.md
```
Expected: Links point to `./README.zh.md`, `./examples/`, `./CONTRIBUTE.md`.

- [ ] **Step 3: Commit**

```bash
git add image-to-prompt-skill/README.md
git commit -m "docs: add English README for image-to-prompt skill

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>"
```

---

### Task 7: Create CONTRIBUTE.zh.md

**Files:**
- Create: `image-to-prompt-skill/CONTRIBUTE.zh.md`

- [ ] **Step 1: Write CONTRIBUTE.zh.md**

```markdown
# 贡献指南

## 如何贡献新案例

1. Fork 本仓库
2. 在 `examples/` 目录下新建一个案例文件，命名格式：`<style-name>-example.md`
3. 按照现有案例的格式编写（必须包含：图片描述、用户输入、Prompt Template、Prompt Case）
4. 确保案例展示的视觉风格与现有案例不重复
5. 提交 Pull Request

## 案例质量标准

每个案例必须包含：
- **User Input** — 图片描述 + 用户请求
- **Prompt Template** — 完整的 10 Section 模板，所有占位符使用 `[ALL_CAPS_SNAKE_CASE]` 格式
- **Prompt Case** — 用实际观察值填充的完整 Prompt

案例必须展示一种**与现有案例不同的视觉风格**。我们不需要 10 个拼贴海报案例。

## 占位符命名审查

- 所有占位符必须全大写 + 下划线：`[SUBJECT_NAME]`
- 不能使用中文或小写：`{员工姓名}`、`[subjectName]` 都是错误的
- 占位符必须具有语义化命名，让人一眼看懂代表什么

## 模板可复用性审查

- 替换占位符后，Prompt 必须在语法和逻辑上保持连贯
- 不能出现"替换后语句不通"的情况
- 案例中的 Template 和 Case 必须一一对应，Section 数量一致

## 分析完整性审查

- 必须覆盖全部 10 个分析维度
- 即使某个维度内容很少（如纯摄影没有文字），也要显式写出"No text elements present"
- 不能省略任何 Section

## 提交流程

```bash
# 1. Fork 仓库并克隆
git clone https://github.com/YOUR_USERNAME/shiny-skills.git

# 2. 创建新分支
git checkout -b add-example-STYLE_NAME

# 3. 添加案例文件
cp template.md examples/MY_STYLE-example.md
# 编辑文件...

# 4. 提交
git add examples/MY_STYLE-example.md
git commit -m "feat: add EXAMPLE_NAME example"

# 5. 推送到你的 Fork 并创建 PR
git push origin add-example-STYLE_NAME
```

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
```

- [ ] **Step 2: Commit**

```bash
git add image-to-prompt-skill/CONTRIBUTE.zh.md
git commit -m "docs: add Chinese contribution guidelines

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>"
```

---

### Task 8: Create CONTRIBUTE.md

**Files:**
- Create: `image-to-prompt-skill/CONTRIBUTE.md`

- [ ] **Step 1: Write CONTRIBUTE.md**

```markdown
# Contribution Guidelines

## How to Contribute New Examples

1. Fork this repository
2. Create a new example file in the `examples/` directory, naming convention: `<style-name>-example.md`
3. Follow the format of existing examples (must include: image description, user input, Prompt Template, Prompt Case)
4. Ensure the example demonstrates a visual style distinct from existing examples
5. Submit a Pull Request

## Example Quality Standards

Every example must include:
- **User Input** — Image description + user request
- **Prompt Template** — Complete 10-section template, all placeholders in `[ALL_CAPS_SNAKE_CASE]` format
- **Prompt Case** — Complete prompt filled with actual observed values

Examples must demonstrate a **visual style different from existing examples**. We don't need 10 collage poster examples.

## Placeholder Naming Review

- All placeholders must be ALL_CAPS + snake_case: `[SUBJECT_NAME]`
- No Chinese or lowercase placeholders: `{员工姓名}` or `[subjectName]` are incorrect
- Placeholders must have semantic names that are self-explanatory

## Template Reusability Review

- After swapping placeholders, the prompt must remain grammatically and logically coherent
- No "broken sentences after substitution" allowed
- Template and Case in each example must have matching sections with identical counts

## Analysis Completeness Review

- Must cover all 10 analysis dimensions
- Even if a dimension has minimal content (e.g., no text in a pure photograph), explicitly state "No text elements present"
- No sections may be omitted

## Submission Workflow

```bash
# 1. Fork and clone
git clone https://github.com/YOUR_USERNAME/shiny-skills.git

# 2. Create a branch
git checkout -b add-example-STYLE_NAME

# 3. Add example file
cp template.md examples/MY_STYLE-example.md
# Edit the file...

# 4. Commit
git add examples/MY_STYLE-example.md
git commit -m "feat: add EXAMPLE_NAME example"

# 5. Push to your fork and open PR
git push origin add-example-STYLE_NAME
```

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
```

- [ ] **Step 2: Commit**

```bash
git add image-to-prompt-skill/CONTRIBUTE.md
git commit -m "docs: add English contribution guidelines

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>"
```

---

### Task 9: Update Root README.zh.md

**Files:**
- Modify: `README.zh.md`

- [ ] **Step 1: Read current root README.zh.md**

Use Read tool to inspect the current content of `README.zh.md`.

- [ ] **Step 2: Add image-to-prompt-skill section**

Insert a new skill section after `image-creation-prompt-skill` and before the "安装" section. Add:

```markdown
---

### 🔍 [image-to-prompt-skill](./image-to-prompt-skill/)

将任意图片逆向拆解为结构化 Prompt 模板和具体案例——上传一张图，即可获得可复用的风格配方。

**输入：**
上传一张图片并说：
```
根据这张图生成 prompt 模板
```

**输出：**
- **Prompt 模板**：带 `[PLACEHOLDER]` 占位符的可复用模板，保存后可用于生成同风格不同主题的图片
- **Prompt 案例**：用当前图片实际内容填充的完整 Prompt，直接粘贴到 Nano Banana、Midjourney、DALL-E 等工具即可使用

→ [完整文档与安装说明](./image-to-prompt-skill/)
```

- [ ] **Step 3: Verify the edit**

Run:
```bash
grep -A 5 "image-to-prompt-skill" README.zh.md
```
Expected: Shows the new skill section with correct relative paths.

- [ ] **Step 4: Commit**

```bash
git add README.zh.md
git commit -m "docs: add image-to-prompt-skill to root README.zh.md

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>"
```

---

### Task 10: Update Root README.md

**Files:**
- Modify: `README.md`

- [ ] **Step 1: Read current root README.md**

Use Read tool to inspect the current content of `README.md`.

- [ ] **Step 2: Add image-to-prompt-skill section**

Insert a new skill section after `image-creation-prompt-skill` and before the "Installation" section. Add:

```markdown
---

### 🔍 [image-to-prompt-skill](./image-to-prompt-skill/)

Reverse-engineer any image into a structured prompt template and concrete case — upload an image, get a reusable style recipe.

**Input:**
Upload an image and say:
```
Generate a prompt template from this image
```

**Output:**
- **Prompt Template**: Reusable template with `[PLACEHOLDER]` variables. Save and adapt for similar images with different subjects.
- **Prompt Case**: Complete prompt filled with actual content from the image. Paste directly into Nano Banana, Midjourney, DALL-E, etc.

→ [Full documentation and installation](./image-to-prompt-skill/)
```

- [ ] **Step 3: Verify the edit**

Run:
```bash
grep -A 5 "image-to-prompt-skill" README.md
```
Expected: Shows the new skill section with correct relative paths.

- [ ] **Step 4: Commit**

```bash
git add README.md
git commit -m "docs: add image-to-prompt-skill to root README.md

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>"
```

---

### Task 11: Final Verification and Push

**Files:**
- All files in `image-to-prompt-skill/`
- `README.zh.md`, `README.md`

- [ ] **Step 1: Verify directory structure**

Run:
```bash
find image-to-prompt-skill -type f | sort
```
Expected:
```
image-to-prompt-skill/CONTRIBUTE.md
image-to-prompt-skill/CONTRIBUTE.zh.md
image-to-prompt-skill/README.md
image-to-prompt-skill/README.zh.md
image-to-prompt-skill/SKILL.md
image-to-prompt-skill/examples/neon-cyberpunk-poster-example.md
image-to-prompt-skill/examples/portrait-photography-example.md
image-to-prompt-skill/examples/urban-collage-poster-example.md
```

- [ ] **Step 2: Verify placeholder naming across all files**

Run:
```bash
grep -rohE '\[[a-zA-Z_]+\]' image-to-prompt-skill/ | grep -vE '^\[[A-Z_]+\]$' | sort -u
```
Expected: Empty output (no lowercase or camelCase placeholders found).

- [ ] **Step 3: Verify all examples have 20 sections (10 template + 10 case)**

Run:
```bash
for f in image-to-prompt-skill/examples/*.md; do echo "$f: $(grep -c '^=== .* ===$' "$f")"; done
```
Expected: Each file shows count = 20.

- [ ] **Step 4: Push to remote**

```bash
git push
```

Expected: All commits pushed to `origin/image-to-prompt`.

---

## Spec Coverage Self-Review

| Spec Section | Implementing Task(s) | Status |
|--------------|---------------------|--------|
| SKILL.md with trigger, 10-step analysis, output spec | Task 1 | Covered |
| Placeholder naming convention `[ALL_CAPS_SNAKE_CASE]` | All tasks, verified in Task 11 | Covered |
| Example: urban-collage-poster (user reference) | Task 2 | Covered |
| Example: neon-cyberpunk-poster | Task 3 | Covered |
| Example: portrait-photography | Task 4 | Covered |
| README.zh.md | Task 5 | Covered |
| README.md | Task 6 | Covered |
| CONTRIBUTE.zh.md | Task 7 | Covered |
| CONTRIBUTE.md | Task 8 | Covered |
| Root README.zh.md updated | Task 9 | Covered |
| Root README.md updated | Task 10 | Covered |
| All files committed and pushed | Task 11 | Covered |

**No gaps found. No placeholders (TBD/TODO) in plan.**
