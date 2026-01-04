---
name: prompt-optimizer
description: Analyze and improve prompts using Anthropic's official Claude 4.x best practices. Use when users ask to improve, optimize, analyze, debug, or review a prompt, when they say a prompt "isn't working", or when they want help writing better prompts for Claude. Covers XML structuring, chain of thought, multishot examples, output formatting, and Claude-specific techniques.
---

# Prompt Optimizer

Analyze and improve prompts for Claude using Anthropic's official best practices.

## Workflow

### 1. Analyze the Prompt
Identify issues against these criteria:
- **Clarity**: Are instructions specific and unambiguous?
- **Structure**: Are components separated with XML tags?
- **Context**: Is purpose/audience/success criteria explained?
- **Framing**: Are instructions positive (do X) vs negative (don't Y)?
- **Examples**: For complex tasks, are diverse examples provided?
- **Output spec**: Is format, length, tone explicitly defined?
- **Reasoning**: Does complex logic request chain of thought?

### 2. Apply Optimization Techniques

**For vague prompts**: Add explicit instructions with modifiers
```
# Before
Summarize this document

# After  
Summarize this document in 3-5 bullet points, focusing on key findings 
and actionable recommendations. Write for a technical audience.
```

**For unstructured prompts**: Add XML tags
```xml
<instructions>
Your core task description here
</instructions>

<context>
Background information, purpose, audience
</context>

<input>
{{user_content}}
</input>

<output_format>
Specify exact format, length, structure
</output_format>
```

**For complex reasoning**: Add chain of thought
```
Before providing your answer, work through your reasoning step by step 
in <thinking> tags. Then provide your final answer in <answer> tags.
```

**For format issues**: Match prompt style to desired output
- Remove markdown from prompt to reduce markdown in output
- Use XML format indicators: "Write in `<response>` tags"
- Provide explicit format specs with examples

### 3. Output Format

Always respond with this exact structure:

```
<analysis>
2-3 sentence assessment of the original prompt's main issues.
</analysis>

<optimized_prompt>
The improved prompt with proper structure, ready to use.
</optimized_prompt>

<changes>
• Change 1: [what] - [why]
• Change 2: [what] - [why]
</changes>

<tip>
One practical tip for using this prompt effectively.
</tip>
```

## Fast Mode (Haiku - cheaper/faster)

For batch processing or cost-sensitive workflows, use this condensed approach:

**Prompt for Haiku:**
```
Improve this prompt for Claude. Return ONLY the optimized prompt, no explanation.

Key fixes to apply:
- Add XML tags to separate sections
- Make instructions explicit and specific  
- Use positive framing (do X, not don't Y)
- Add output format specification

Original prompt:
{{prompt}}
```

**When to use Fast Mode:**
- Batch processing many prompts
- Quick iterations during development
- Cost-sensitive automation workflows (n8n, Zapier)
- When you just need the improved prompt, not the analysis

**When to use Full Mode (Sonnet/Opus):**
- Learning why changes improve prompts
- Complex prompts needing detailed analysis
- When you need the changes list for documentation

## Key Principles

### Be Explicit
Claude 4.x follows instructions precisely. Specify exactly what you want.

**Less effective**: `Create a dashboard`
**More effective**: `Create a dashboard with filtering, sorting, and export features. Include data visualizations and responsive design.`

### Provide Context
Explain WHY instructions matter—purpose, audience, success criteria.

**Less effective**: `Never use ellipses`
**More effective**: `Responses will be read by text-to-speech, so avoid ellipses which the engine cannot pronounce.`

### Use Positive Framing
Say what TO do, not what NOT to do.

**Less effective**: `Don't use markdown`
**More effective**: `Write in flowing prose paragraphs`

### Structure with XML
Use tags to separate components: `<instructions>`, `<context>`, `<examples>`, `<input>`, `<output_format>`

### Include Examples for Complex Tasks
3-5 diverse examples showing input→output pattern significantly improve accuracy.

## Reference

For detailed techniques, consult: `references/anthropic-best-practices.md`

Covers:
- XML tag structure and best practices
- Chain of thought implementation patterns
- Multishot prompting guidelines
- Output format control techniques
- Long context document handling
- Claude 4.x specific optimizations
- Common anti-patterns and fixes
