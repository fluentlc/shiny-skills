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
