# image-to-prompt Skill Design Spec

## 1. Overview

**Goal:** Create a new Claude Skill that accepts an uploaded image from the user and produces two artifacts:

1. **Prompt Template** — A reusable structured prompt with `[PLACEHOLDER]` variables that users can save and adapt for generating similar images with different subjects/content.
2. **Prompt Case** — The concrete prompt with placeholders filled using the actual content observed in the input image.

**Position in project:** Sibling to `image-creation-prompt-skill/` at repo root level: `image-to-prompt-skill/`.

**Relationship to existing skill:**
- `image-creation-prompt-skill` = forward: text description → structured prompt (creator)
- `image-to-prompt-skill` = reverse: image → structured prompt + reusable template (reverse engineer)

Both skills share the same structured prompt convention (`=== Section ===` headers) so users can seamlessly move between them. This skill outputs 10 sections vs. the existing skill's 6, because reverse-engineering an image requires more analytical dimensions than forward-generation from a text description.

---

## 2. Directory Structure

```
image-to-prompt-skill/
├── SKILL.md                          # Core skill definition: trigger, 10-step analysis, output spec
├── README.md                         # English usage documentation
├── README.zh.md                      # Chinese usage documentation
├── examples/                         # Few-shot examples for Agent learning
│   ├── urban-collage-poster-example.md
│   ├── neon-cyberpunk-poster-example.md
│   └── portrait-photography-example.md
├── CONTRIBUTE.md
└── CONTRIBUTE.zh.md
```

No `styles/` directory. This skill does not match against a predefined style registry. Instead, it performs free-form visual analysis.

---

## 3. SKILL.md Design

### 3.1 Trigger Conditions

The skill activates when:
- User uploads an image (via base64, file path, or URL) and asks for a prompt
- User explicitly requests: "根据这张图生成 prompt", "reverse engineer this image", "分析这张图片的风格", "拆解这张图的结构"
- Keywords: "image to prompt", "图片转 prompt", "prompt 模板", "逆向图片"

### 3.2 10-Step Visual Analysis Framework

The Agent must systematically analyze the image across 10 dimensions before generating output:

| Step | Dimension | What to Extract |
|------|-----------|-----------------|
| 1 | **Overall Style** | Art movement, visual genre, aesthetic label (e.g., "graffiti collage poster", "minimalist flat illustration") |
| 2 | **Color Scheme** | Primary/secondary colors, contrast level, saturation, palette type (monochrome, complementary, analogous, etc.) |
| 3 | **Main Subject** | Central figure/object: identity, pose, expression, clothing, accessories, physical traits |
| 4 | **Background Design** | Environment, depth of field, background elements, layering, spatial relationship to subject |
| 5 | **Text & Typography** | All visible text content, font styles, sizes, orientations, languages, placement strategy |
| 6 | **Composition & Perspective** | Framing, rule of thirds, symmetry/asymmetry, diagonal lines, camera angle, focal point, visual hierarchy |
| 7 | **Material & Texture** | Surface qualities: paper, metal, fabric, digital smoothness, brush strokes, torn edges, grain |
| 8 | **Lighting & Mood** | Light direction, intensity, shadows, highlights, emotional tone, atmosphere |
| 9 | **Decorative & Auxiliary Elements** | Icons, borders, geometric shapes, patterns, filters, overlays, vignettes |
| 10 | **Quality & Technical Parameters** | Estimated aspect ratio, resolution cues, suspected AI model parameters (e.g., `--ar 9:16 --v 5 --style raw`) |

### 3.3 Output Format

Two code blocks are produced in a single response.

#### Block 1: Prompt Template

```
=== [Style Name] ===
[Style description with placeholders for adaptable elements]

=== Color Scheme ===
[Color palette description with [PRIMARY_COLOR], [SECONDARY_COLOR] placeholders]

=== Main Subject ===
[Subject template with [SUBJECT_NAME], [AGE], [POSE], [CLOTHING] placeholders]

=== Background Design ===
[Background template with [SETTING], [DEPTH], [BG_ELEMENTS] placeholders]

=== Text & Typography ===
[Text template with [HEADLINE], [BODY_TEXT], [FONT_STYLE] placeholders]

=== Composition & Perspective ===
[Composition template with [FRAMING], [PERSPECTIVE], [FOCAL_POINT] placeholders]

=== Material & Texture ===
[Material template with [SURFACE_TYPE], [TEXTURE_DETAIL] placeholders]

=== Lighting & Mood ===
[Lighting template with [LIGHT_DIRECTION], [MOOD] placeholders]

=== Decorative Elements ===
[Decorative template with [DECOR_TYPE], [PATTERN] placeholders]

=== Quality & Technical ===
[Quality tags with [ASPECT_RATIO], [MODEL_PARAMS] placeholders]
```

#### Block 2: Prompt Case

Same 10 sections, but all placeholders are replaced with actual values observed in the input image.

### 3.4 Placeholder Naming Convention

- All caps, snake_case, wrapped in brackets: `[SUBJECT_NAME]`, `[PRIMARY_COLOR]`
- Semantic naming: the placeholder name describes what it represents
- Language-agnostic: placeholders use English for universal readability since the skill is open-source
- Common reusable placeholders (predefined in SKILL.md):
  - `[SUBJECT_NAME]` / `[SUBJECT_TYPE]`
  - `[AGE]` / `[GENDER]` / `[POSE]` / `[EXPRESSION]`
  - `[CLOTHING]` / `[ACCESSORIES]` / `[HAIR_STYLE]`
  - `[PRIMARY_COLOR]` / `[SECONDARY_COLOR]` / `[ACCENT_COLOR]`
  - `[SETTING]` / `[BG_ELEMENTS]` / `[DEPTH_OF_FIELD]`
  - `[HEADLINE]` / `[BODY_TEXT]` / `[FONT_STYLE]`
  - `[LIGHT_DIRECTION]` / `[LIGHT_QUALITY]` / `[MOOD]`
  - `[ASPECT_RATIO]` / `[MODEL_VERSION]` / `[STYLE_PARAM]`
  - `[ART_STYLE]` / `[TEXTURE_TYPE]` / `[DECOR_ELEMENTS]`

### 3.5 Content Quality Rules

1. **Be specific, not vague.** Instead of "modern design," write "asymmetrical layout with strong diagonal lines and overlapping geometric shapes."
2. **Preserve proportions and relationships.** If the subject occupies 30% of the frame and is positioned left-of-center, say so.
3. **Distinguish observed from inferred.** Observed: "black and orange color scheme." Inferred: "likely generated with --v 5 --style raw."
4. **Template must be truly reusable.** A user should be able to swap `[SUBJECT_NAME]` and `[SUBJECT_TYPE]` and get a coherent new prompt for a different subject in the same style.
5. **Quality tags go last.** Always end with technical/quality parameters so they can be easily copied to image generators.

---

## 4. Examples Design

### 4.1 Example File Structure

Each `examples/<name>-example.md` contains:

```markdown
# Example: [Descriptive Name]

## User Input

[Image reference or path]
User request: "根据这张图片生成 prompt 模板和案例"

## Generated Prompt Template

=== [Style Name] ===
...

## Generated Prompt Case

=== [Style Name] ===
...
```

### 4.2 Example Coverage

| Example | Style | Why Included |
|---------|-------|--------------|
| `urban-collage-poster-example.md` | Graffiti collage poster | The reference case provided by the user. Complex multi-layer composition with text, portrait, and urban elements. |
| `neon-cyberpunk-poster-example.md` | Cyberpunk neon poster | High-contrast futuristic style with distinct lighting and glow effects. Tests lighting analysis. |
| `portrait-photography-example.md` | Studio portrait photography | Natural/realistic subject with minimal graphic elements. Tests subject analysis without text distractions. |

Each example demonstrates different analysis emphases: poster (text-heavy, graphic), cyberpunk (lighting-heavy, atmospheric), portrait (subject-heavy, minimal).

---

## 5. README Documentation

### README.zh.md Content Outline

1. **What is this skill?** — Brief description of reverse-engineering images into prompts
2. **Input:** Upload an image + request prompt generation
3. **Output:** Two code blocks (Template + Case)
4. **Installation** — Same `cp -r` pattern as existing skill
5. **Usage** — Example workflow
6. **How it works** — Brief mention of 10-step analysis
7. **Examples** — Link to `examples/` directory
8. **Request analysis** — How to request analysis of a new image type
9. **Contribute** — Link to CONTRIBUTE.zh.md
10. **License** — MIT

### README.md Content Outline

Mirror of README.zh.md in English.

---

## 6. CONTRIBUTE Guidelines

### CONTRIBUTE.zh.md Content Outline

1. **如何贡献新案例** — Add a new example file following the established format
2. **案例质量标准** — Must include: image source, user input, template, case; must demonstrate a distinct visual style not already covered
3. **提交流程** — Fork → add example → PR
4. **审查标准** — Placeholder naming consistency, template reusability, analysis completeness

---

## 7. Open Questions (Resolved)

| Question | Decision |
|----------|----------|
| Placeholder language? | English, all-caps snake_case (`[SUBJECT_NAME]`) — for universal open-source readability |
| Analysis steps? | 10-step complete framework (no tiered optional steps) — comprehensive coverage is the skill's value |
| Output sections? | Exactly 10 sections matching the 10 analysis steps, plus a style name header section |
| Style registry? | None. Free-form analysis. No `styles/` directory. |
| Relationship to image-creation-prompt-skill? | Sibling skill, reverse direction, same output format convention |

---

## 8. Acceptance Criteria

- [ ] `image-to-prompt-skill/SKILL.md` exists and contains complete trigger, analysis, and output specs
- [ ] `image-to-prompt-skill/examples/urban-collage-poster-example.md` matches the user's reference case exactly
- [ ] `image-to-prompt-skill/examples/` contains 2 additional diverse examples
- [ ] `image-to-prompt-skill/README.md` and `README.zh.md` are complete and consistent
- [ ] `image-to-prompt-skill/CONTRIBUTE.md` and `CONTRIBUTE.zh.md` exist
- [ ] Root `README.zh.md` and `README.md` are updated to list the new skill
- [ ] All placeholder names follow the `[ALL_CAPS_SNAKE_CASE]` convention
- [ ] All files are committed and pushed
