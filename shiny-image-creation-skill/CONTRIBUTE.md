# Contributing to shiny-skills

[中文版](./CONTRIBUTE.zh.md)

Welcome! Contributions of new style templates are the primary way to grow this project.

## Contributing a New Style Template

### Steps

1. Fork this repository
2. In the target skill's `SKILL.md`, find the `## Style Templates` section and append your new template
3. Add at least one complete example (user input + generated output) to the `examples/` directory inside the skill folder
4. Update the style table in `README.md`
5. Open a Pull Request describing the style's intended use cases and design logic

### Required Template Sections

Each style template must include all of the following:

| Section | Description |
|---------|-------------|
| **Opening Line** | Style declaration with placeholders for topic and aspect ratio |
| **TITLE STYLE** | Font style, color, container shape (bubble / banner / cloud, etc.) |
| **SCENE & LAYOUT** | Background description + overall composition logic (roadmap / staircase / radial, etc.) |
| **MAIN CONTENT** | Per-step / per-section structure, including connection arrow descriptions |
| **VISUAL STYLE** | Material, render technique, color palette |
| **DECORATIVE ELEMENTS** | Elements to fill negative space |
| **MOOD** | Atmosphere keywords |
| **Quality** | Quality tags (resolution, detail level, style modifiers) |
| **Fill-in rules** | Explains the aesthetic logic so Claude knows how to make judgment calls when filling in content |

### Template Format

```markdown
### Template N: [Chinese Style Name] ([English Name])

**Opening Line:**
\```
[Style declaration], [aspect_ratio], explaining [topic].
\```

**Sections:**

\```
=== TITLE STYLE ===
...

=== SCENE & LAYOUT ===
...

=== MAIN CONTENT ===
[For each step, use STEP_N format]

[STEP_N]
Visual: ...
Action: ...
Label: ...
Connection: ...

=== VISUAL STYLE ===
...

=== DECORATIVE ELEMENTS ===
...

=== MOOD ===
...

Quality: ...
\```

**Fill-in rules:**
- [Aesthetic rule 1]
- [Aesthetic rule 2]
- [Aesthetic rule 3]
```

### What Makes a Good Template

- **Distinct visual identity**: Clear color palette, material feel, and typographic style
- **Clear use cases**: Explain what type of content or topic this style suits best
- **Actionable fill-in rules**: Don't just describe the look — tell Claude how to make decisions when filling in content
- **Validated by real output**: The template should be derived from a prompt that actually produced good results, not designed from scratch

## Other Ways to Contribute

- Open an Issue to report cases where the generated prompt produced poor results
- Add more examples to the `examples/` directory
- Improve the Fill-in rules of existing templates
