# Style Template: 街景 AR 标注图风格 (Street Scene AR Annotation Style)

**Input format:** `[location] AR标注风格, [aspect_ratio]` or `生成[location]标注风格的图片, [aspect_ratio]`

> ⚠️ This style generates an AR-annotated location photograph. Input is a place/scene name, not an educational topic.

**Opening Line:**
```
Generate a photorealistic street-level or aerial photo of [location]. Then overlay AR-style information annotations on the image.
```

**Sections:**

```
=== TOPIC ===
explaining [location] AR标注

=== MAIN_TITLE ===
[Location Name] AR标注

=== SUBTITLE_TEXT ===
[Location] [导览/景观/结构/经典] AR导览图

=== SCENE_DESCRIPTION ===
Generate a photorealistic [street-level / aerial / bird's-eye] photo of [location]. Then overlay AR-style information annotations on the image. Each annotation has a thin connecting line from the label to the landmark. Use a clean, modern AR UI design with frosted glass effect cards, white text, and small icons.

=== BACKGROUND_STYLE ===
[Describe the scene's atmosphere: lighting quality, key natural elements, architectural style, seasonal details, ambient activity, color temperature, weather, distance and depth of key landmarks]

=== SHORT_TEXT ===
[List 4–6 key annotation labels, separated by ｜ — e.g., landmark names, structural components, or points of interest]

=== DIALOGUE_TEXT ===
N/A

=== NARRATION_TEXT ===
[One to two sentences describing the location's cultural, historical, or technical significance in Chinese]

=== NUMBER ===
[N] annotation cards (typically 4–6 for natural scenes, 6–10 for complex structures)

=== SIZE ===
medium-sized frosted glass cards (80×40px), 1.5pt connector lines, 14pt semi-bold white font

=== POSITION ===
strategically anchored to key landmarks across wide landscape framing ([aspect_ratio]), avoiding occlusion of main visual flow

| 8k, ultra-detailed, photorealistic, cinematic lighting, AR interface overlay, frosted glass UI, clean vector icons, sharp focus, natural color grading, atmospheric perspective, masterpiece, best quality
```

**Fill-in rules:**
- Annotation cards should use frosted glass (semi-transparent white) with minimal text — label + 1 icon maximum per card
- Connector lines should be thin (1–1.5pt), straight or gently curved, never overlapping each other
- Background photo must feel photorealistic and atmospheric — not a diagram
- Annotations should cover spatially distinct areas of the image (left, center, right, foreground, background) to maximize readability
- The SHORT_TEXT list becomes the annotation labels — choose 4–6 most recognizable or significant features
