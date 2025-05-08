# Feature Specification: Implement OpenAI Reasoning Models

## High Level Objective
Currently, our system uses standard OpenAI chat and text completion models (e.g. `gpt-4o`, `gpt-4.1`) for generating responses. This feature will extend the system to support dedicated OpenAI reasoning models (e.g. `o4-mini`, `o3`) for tasks requiring advanced chain-of-thought and multi-step reasoning.

Benefits:
- Enables richer chain-of-thought reasoning and transparency.
- Improves accuracy on complex, multi-step tasks.
- Allows model selection based on reasoning requirements.
- Maintains backward compatibility by defaulting to existing models when reasoning is not required.
- Facilitates experimentation with new OpenAI reasoning endpoints.

## Type Changes

### Configuration Module
**File**: `src/config/openai_models.py`

1. Extend the `OpenAIModel` enum:
```python
class OpenAIModel(str, Enum):
    GPT_4O = "gpt-4o"
    O4_MINI = "o4-mini"
    O3 = "o3"
```

2. Define new defaults:
```python
DEFAULT_MODEL = OpenAIModel.GPT_4O
REASONING_MODEL = OpenAIModel.O4_MINI
```

### API Module
**File**: `src/api/openai_client.py`

1. Update `OpenAIClient.generate` to accept a `model_type` override:
```python
def generate(self, prompt: str, model_type: OpenAIModel = None, **kwargs):
    selected = model_type or self.model
    return openai.ChatCompletion.create(
        model=selected.value,
        messages=[{"role": "user", "content": prompt}],
        **kwargs
    )
```

## Method Changes

### Reasoning Workflow Module
**File**: `src/modules/reasoning/workflow.py`

1. Add a new function `chain_of_thought`:
```python
def chain_of_thought(prompt: str, steps: int = 3) -> List[str]:
    responses = []
    for i in range(steps):
        resp = openai_client.generate(
            f"Step {i+1}: {prompt}", model_type=REASONING_MODEL
        )
        content = resp.choices[0].message.content
        responses.append(content)
        prompt = content
    return responses
```

2. Implement error handling for rate limits and retries.

### Integration Module
**File**: `src/modules/task_handler.py`

1. Route tasks requiring reasoning:
```python
if task.requires_reasoning:
    result = chain_of_thought(task.prompt, task.reasoning_steps)
else:
    result = openai_client.generate(task.prompt)
```

## Test Changes

### Configuration Tests
**File**: `tests/test_openai_models.py`

- Test new enum entries and default assignments.

### Client Tests
**File**: `tests/test_openai_client.py`

- Mock tests to verify `model_type` override.

### Workflow Tests
**File**: `tests/test_reasoning_workflow.py`

- Test `chain_of_thought` returns correct number of steps.
- Simulate rate limit and retry behavior.

## Self Validation

1. **Manual Testing**:
   - Run reasoning workflow on a simple prompt and verify sequential reasoning steps.

2. **Automated Testing**:
   - Execute `pytest tests/ -q` and verify all tests pass.

## README Update
**File**: `README.md`

1. Add `## OpenAI Reasoning Models` section with usage examples:
```markdown
export OPENAI_MODEL=o4-mini
```
2. Update Quickstart usage:
```bash
python main.py --prompt "Prove Pythagorean theorem" --steps 4 --reasoning
```
