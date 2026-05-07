# image-to-prompt-skill

[English](./README.md)

一个将上传的图片逆向拆解为结构化 Prompt 模板和具体案例的 Skill。

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
=== Overall Style ===
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

## 请求新案例

遇到一种很好看的图片风格，想让它被收录为分析案例？提一个 Issue 并附上图片，贡献者会为你生成完整的 Prompt 模板和案例。

## 贡献

参见 [`CONTRIBUTE.zh.md`](./CONTRIBUTE.zh.md)。

## License

MIT
