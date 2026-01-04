# Anthropic Prompt Engineering Best Practices

Comprehensive reference for Claude 4.x prompt optimization techniques based on official Anthropic documentation.

## Core Principles

### 1. Be Explicit with Instructions
Claude 4.x models follow instructions precisely. Be specific about desired output.

**Less effective:**
```
Create an analytics dashboard
```

**More effective:**
```
Create an analytics dashboard. Include as many relevant features and interactions as possible. Go beyond the basics to create a fully-featured implementation.
```

### 2. Provide Context (the WHY)
Explain motivation behind instructions to help Claude understand goals.

**Less effective:**
```
NEVER use ellipses
```

**More effective:**
```
Your response will be read aloud by a text-to-speech engine, so never use ellipses since the text-to-speech engine will not know how to pronounce them.
```

### 3. Use Positive Framing
Tell Claude what TO do, not what NOT to do.

**Less effective:**
```
Do not use markdown in your response
```

**More effective:**
```
Your response should be composed of smoothly flowing prose paragraphs.
```

### 4. Be Vigilant with Examples
Claude 4.x pays close attention to examples. Ensure they align with desired behaviors and minimize undesired patterns.

## XML Tag Structure

### Why Use XML Tags
- **Clarity**: Separate prompt components clearly
- **Accuracy**: Reduce misinterpretation
- **Flexibility**: Easy to modify sections
- **Parseability**: Extract specific output parts

### Recommended Tags
| Tag | Purpose |
|-----|---------|
| `<instructions>` | Core task directions |
| `<context>` | Background information |
| `<examples>` | Input/output demonstrations |
| `<input>` | User-provided content |
| `<output_format>` | Response structure spec |
| `<constraints>` | Limitations/boundaries |
| `<thinking>` | Chain of thought reasoning |
| `<answer>` | Final response |

### Tagging Best Practices
1. **Consistency**: Use same tag names throughout
2. **Reference tags**: "Using the data in `<data>` tags..."
3. **Nest hierarchically**: `<outer><inner></inner></outer>`
4. **Use format indicators**: "Write response in `<response>` tags"

## Chain of Thought (CoT)

### When to Use
- Complex reasoning tasks
- Multi-step problems
- Mathematical calculations
- Analysis requiring evidence

### Implementation Patterns

**Basic CoT:**
```
Think step by step before providing your answer.
```

**Structured CoT:**
```
Before answering, work through your reasoning in <thinking> tags.
Then provide your final answer in <answer> tags.
```

**Guided CoT:**
```
Follow these steps:
1. Identify the key components
2. Analyze each component
3. Synthesize findings
4. Draw conclusions
```

## Multishot Prompting (Examples)

### Guidelines
- Include 3-5 diverse examples for complex tasks
- Examples should demonstrate input→output pattern
- Cover edge cases and variations
- Format consistently

### Example Structure
```xml
<examples>
  <example>
    <input>Example input 1</input>
    <output>Example output 1</output>
  </example>
  <example>
    <input>Example input 2</input>
    <output>Example output 2</output>
  </example>
</examples>
```

## Output Format Control

### Techniques
1. **Explicit format specification**:
   ```
   Respond in JSON format with these fields: name, description, priority
   ```

2. **XML format indicators**:
   ```
   Write your analysis in <analysis> tags
   ```

3. **Match prompt style to output**:
   Remove markdown from prompts to reduce markdown in output

4. **Detailed formatting prompts**:
   ```xml
   <formatting>
   Use clear, flowing prose. Reserve markdown only for:
   - `inline code`
   - Code blocks (```...```)
   - Simple headings (##, ###)
   Avoid bullet points unless presenting truly discrete items.
   </formatting>
   ```

## Long Context Tips

### Document Placement
- Place long documents (20K+ tokens) at TOP of prompt
- Put queries/instructions AFTER documents
- Queries at end can improve quality by 30%

### Document Structure
```xml
<documents>
  <document index="1">
    <source>document_name.pdf</source>
    <document_content>
      {{DOCUMENT_CONTENT}}
    </document_content>
  </document>
</documents>
```

## Prompt Chaining

### When to Chain
- Multi-step tasks
- Complex instructions that may be missed
- When output verification is needed
- Parallel independent subtasks

### Principles
- Keep subtasks simple and focused
- Use output of one prompt as input to next
- Verify outputs before proceeding

## Claude 4.x Specific Guidance

### Verbosity Control
Claude 4.5 tends toward efficiency. For more updates:
```
After completing a task that involves tool use, provide a quick summary of the work you've done.
```

### Tool Usage
Be explicit about taking action:
```
Implement changes rather than only suggesting them. If the user's intent is unclear, infer the most useful likely action and proceed.
```

### Parallel Tool Calling
```xml
<use_parallel_tool_calls>
If you intend to call multiple tools and there are no dependencies between the calls, make all independent tool calls in parallel.
</use_parallel_tool_calls>
```

### Minimize Over-Engineering
```
Avoid over-engineering. Only make changes that are directly requested or clearly necessary. Keep solutions simple and focused.
```

## Common Anti-Patterns

### Avoid
1. **Vague instructions**: "Make it better"
2. **Negative-only constraints**: "Don't use X, Y, Z"
3. **Conflicting examples**: Examples that show different patterns
4. **Over-prompting**: Instructions for obvious things
5. **Missing context**: No explanation of purpose/audience
6. **Inconsistent formatting**: Mixed tag names or structures

### Fix Patterns
| Problem | Solution |
|---------|----------|
| Output too verbose | Specify length/format explicitly |
| Wrong format | Provide example of exact format |
| Misses requirements | Use numbered checklist |
| Inconsistent | Add more diverse examples |
| Too literal | Add context about intent |

## Quality Checklist

Before finalizing a prompt, verify:

- [ ] Clear task description with success criteria
- [ ] Context explains WHY (purpose, audience)
- [ ] Instructions use positive framing
- [ ] XML tags separate components
- [ ] Examples demonstrate desired output (if complex)
- [ ] Output format explicitly specified
- [ ] CoT requested for complex reasoning
- [ ] Constraints are specific and actionable
