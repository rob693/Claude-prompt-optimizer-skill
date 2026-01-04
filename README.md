# Prompt Optimizer Skill for Claude

A skill for Claude (via Claude.ai or Claude Code) that analyzes and improves prompts using Anthropic's official best practices for Claude 4.x models.

## What is this?

This is a **Claude Skill** — a set of instructions and reference materials that Claude can use to perform specialized tasks. When installed, Claude gains the ability to systematically analyze and optimize prompts for better results.

## Features

- **Structured Analysis**: Evaluates prompts against clarity, structure, context, framing, examples, output specification, and reasoning criteria
- **XML Tag Optimization**: Restructures prompts using proper XML tag separation
- **Chain of Thought Integration**: Adds reasoning structures for complex tasks
- **Positive Framing**: Converts "don't do X" instructions to "do Y" format
- **Output Format Control**: Specifies exact formats for consistent results
- **Fast Mode**: Condensed approach for batch processing with Haiku

## Installation

### For Claude.ai (Projects)

1. Create a new Project in Claude.ai
2. Add the contents of `SKILL.md` to your Project's custom instructions
3. Optionally add `references/anthropic-best-practices.md` as a project document for deeper reference

### For Claude Code

1. Copy the `prompt-optimizer` folder to your skills directory:
   ```bash
   # User skills location
   ~/.claude/skills/prompt-optimizer/
   ```

2. Or include in a project's `.claude/skills/` directory

## Usage

Once installed, simply ask Claude to optimize a prompt:

```
Using the prompt optimizer skill, improve this prompt:
"summarize this document"
```

Claude will respond with:
- **Analysis**: Assessment of the original prompt's issues
- **Optimized Prompt**: The improved version, ready to use
- **Changes**: What was changed and why
- **Tip**: Practical advice for using the optimized prompt

### Example

**Before:**
```
Write a blog post about AI
```

**After:**
```xml
<instructions>
Write a blog post about AI trends in 2024. Focus on practical applications 
for small businesses. Aim for 800-1000 words.
</instructions>

<context>
Target audience: Small business owners with limited technical background.
Tone: Accessible and practical, avoiding jargon.
</context>

<output_format>
Structure with:
- Engaging headline
- Brief introduction (2-3 sentences)
- 3-4 main sections with subheadings
- Actionable conclusion
</output_format>
```

## Key Optimization Principles

1. **Be Explicit**: Claude follows instructions precisely — specify exactly what you want
2. **Provide Context**: Explain WHY instructions matter (purpose, audience, success criteria)
3. **Use Positive Framing**: Say what TO do, not what NOT to do
4. **Structure with XML**: Separate components using tags like `<instructions>`, `<context>`, `<output_format>`
5. **Include Examples**: For complex tasks, 3-5 diverse examples improve accuracy significantly

## Files

```
prompt-optimizer/
├── README.md                              # This file
├── SKILL.md                               # Main skill instructions
└── references/
    └── anthropic-best-practices.md        # Detailed techniques reference
```

## Contributing

Contributions welcome! Feel free to:
- Add more optimization patterns
- Improve examples
- Update for new Claude model versions
- Add language-specific variations

## License

MIT License — use freely, attribution appreciated.

## Credits

Based on [Anthropic's official prompt engineering documentation](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering).

---

*Built for sharing knowledge about effective Claude prompting.*
