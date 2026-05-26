---
title: "Output Contracts"
type: concept
tags: [prompt-engineering, structured-output, consistency, specification, design-patterns]
created: 2026-05-26
updated: 2026-05-26
sources: ["raw/The prompting playbook_zh.md"]
confidence: high
---

## Definition

An output contract is an explicit specification of the exact format a language model should produce, including structure, schema, delimiters, and termination conditions. It bridges [[concepts/prompt-engineering]] and API configuration to ensure consistent, parseable outputs.

## How It Works

**Two-Layer Approach**:

### Layer 1: Prompt Instruction
```xml
<output_format>
Return your response wrapped in <response> tags.
Use XML tags for structured data.
Always close all tags properly.
</output_format>
```

### Layer 2: API Configuration
Use stop sequences to enforce termination:
```python
api_call(
    prompt=prompt,
    stop_sequences=["</response>"]  # Model stops here
)
```

**Benefits of both layers**:
- Prompt makes contract visible to model (helps it comply)
- Stop sequence prevents token waste from over-generation
- Parser knows exactly where valid output ends

## Key Parameters

- **Schema specification** — XML tags, JSON structure, markdown sections
- **Field requirements** — Which fields must be present, which are optional
- **Data types** — String, number, array, nested objects
- **Boundaries** — Where output should start and end
- **Escaping rules** — How to handle special characters
- **Stop sequences** — API-level termination signals

## When To Use

- **Structured outputs needed** — JSON APIs, database inserts, downstream processing
- **Multiple test cases** — When consistency across runs matters
- **Streaming responses** — Parser needs to know where chunks end
- **Integration with code** — Systems parsing model output programmatically
- **Customer service bots** — Ensures user sees predictable format (not messy reasoning traces)

## Risks & Pitfalls

- **Over-specification** — Rigid format forces model to truncate important information
- **Format breaking** — Model sometimes violates contract if it conflicts with reasoning needs
- **Parsing fragility** — Stop sequences work most but not 100% of time
- **Context loss** — Tight formatting requirements may cause model to omit nuance
- **Debugging difficulty** — Hard to see model's actual reasoning if only structured output shown

## Anti-Pattern: Overly Rigid Output

```xml
<!-- ❌ Too strict - might force truncation -->
<response>
  <answer><!-- Max 10 words only -->
  <confidence><!-- Must be 0-1 -->
</response>
```

**Better approach**: Keep structure but allow flexibility in content:
```xml
<!-- ✓ Structured but flexible -->
<response>
  <answer><!-- Full answer, as long as needed -->
  <reasoning><!-- Explain your thinking -->
  <confidence_score><!-- 0-1 scale -->
</response>
```

## Implementation

**Option A: XML in Prompt + Stop Sequence**
```python
prompt = """Return response in XML format:
<response>
  <result>...</result>
  <explanation>...</explanation>
</response>
"""
response = client.messages.create(
    prompt=prompt,
    stop_sequences=["</response>"]
)
```

**Option B: Structured Output Mode** (Claude 3.5+)
```python
response = client.messages.create(
    prompt=prompt,
    extra_headers={"anthropic-beta": "structured-output-v1"},
    response_schema={
        "type": "object",
        "properties": {
            "result": {"type": "string"},
            "confidence": {"type": "number"}
        }
    }
)
```

## Nested Structures

For complex outputs, contract can be hierarchical:
```json
{
  "schedule": {
    "shifts": [
      {
        "employee": "string",
        "day": "string", 
        "hours": "integer"
      }
    ]
  },
  "violations": [
    {
      "type": "string",
      "severity": "string",
      "details": "string"
    }
  ]
}
```

## Related Concepts

- [[concepts/prompt-engineering]] — Output contract is critical part of prompt design
- [[concepts/evaluation-frameworks]] — Evaluators often check output format validity
- [[concepts/agentic-loops]] — Each stage output contract must match next stage input contract
- [[concepts/output-formats]] — Generalized concept of how to present information
- [[concepts/tool-use-patterns]] — Tools often expect specific input format from model

## Sources

- [[wiki/summaries/the-prompting-playbook-zh]] — Customer service bot example: stop sequences enforced XML response format for consistency
