# shiny-skills ✨

[English](./README.md)

一个精心策划的 Claude Code Skill 库——每个 Skill 都能让人眼前一亮，把平淡无奇的任务变成令人惊喜的体验。

## 什么是 Skill？

**Skill** 是一个 SKILL.md 文件，Claude Code 会自动识别它。当用户的请求匹配到 Skill 的触发条件时，Claude 会加载该 Skill 并按其指引执行——无需插件、无需配置，只需将目录放入 `~/.claude/skills/` 即可。

## Skill 列表

| Skill | 功能 |
|-------|------|
| [shiny-image-creation-skill](./shiny-image-creation-skill/) | 将一句话描述转化为结构化的 AI 绘图 Prompt，支持 27+ 种视觉风格 |

> 持续新增中，欢迎贡献。

## 安装

```bash
git clone https://github.com/fluentlc/shiny-skills.git

# 安装某个 Skill
cp -r shiny-skills/<skill-name> ~/.claude/skills/
```

每个 Skill 目录内都有独立的 README，包含详细的使用说明。

## 贡献

想添加新的 Skill？欢迎提 PR——任何能让人眼前一亮的 Skill 都欢迎加入。

## License

MIT
