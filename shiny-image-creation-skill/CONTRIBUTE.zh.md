# 贡献指南

[English](./CONTRIBUTE.md)

欢迎为 shiny-skills 贡献新的风格模板！

## 贡献新风格模板

### 步骤

1. Fork 此仓库
2. 在 `styles/` 目录创建新的风格模板文件（如 `styles/my-style.md`）
3. 在 `examples/` 目录添加至少一个完整示例（如 `examples/my-style-example.md`），包含用户输入和生成的 Prompt
4. 在 `gallery/` 目录添加一张代表性的生成图片（如 `gallery/my-style.png`），用第 3 步的 Prompt 生成
5. 更新 `SKILL.md` 的风格注册表以及 `README.md` / `README.zh.md` 中的风格列表
6. 提交 Pull Request，描述新风格的适用场景和设计逻辑

### 风格模板结构要求

每个风格模板必须包含以下部分：

| 部分 | 说明 |
|------|------|
| **Opening Line** | 开篇声明行，确立风格基调、主题占位符和比例 |
| **TITLE STYLE** | 标题字体风格、颜色、容器形状（气泡/横幅/云朵等） |
| **SCENE & LAYOUT** | 背景描述 + 整体构图逻辑（路线图/阶梯/辐射等） |
| **MAIN CONTENT** | 各步骤/内容块的结构，含连接方式说明 |
| **VISUAL STYLE** | 材质、渲染方式、配色方案 |
| **DECORATIVE ELEMENTS** | 填充负空间的装饰元素 |
| **MOOD** | 氛围关键词列表 |
| **Quality** | 质量标签（分辨率、细节、风格修饰词） |
| **Fill-in rules** | 解释此风格的审美逻辑，指导内容填充时的判断依据 |

### 模板格式示例

```markdown
### Template N: [风格中文名] ([English Name])

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
- [审美规则1]
- [审美规则2]
- [审美规则3]
```

### 好的风格模板的标准

- **视觉特征明确**：有清晰的配色方案、材质感、排版风格
- **适用场景清晰**：说明什么类型的主题适合使用此风格
- **Fill-in rules 有指导意义**：不只是描述风格，而是告诉 Claude 在填充内容时如何做判断
- **有真实示例验证**：模板来源于实际生成效果好的 Prompt，而非凭空设计

## 其他贡献方式

- 提交 Issue 反馈生成效果不佳的案例
- 补充 `examples/` 目录中的示例，或向 `gallery/` 添加生成图片
- 改进现有模板的 Fill-in rules
