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
