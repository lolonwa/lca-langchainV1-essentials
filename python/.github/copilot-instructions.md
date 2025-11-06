# LangChain Essentials Python - AI Agent Guide

## Core Architecture

- Progressive learning path through Jupyter notebooks (`L1-L9.ipynb`)
- Each notebook demonstrates specific LangChain capabilities
- SQL agents in `studio/` showcase production patterns

## Key Patterns

### Agent Creation

```python
# Standard pattern (see L1_fast_agent.ipynb)
agent = create_agent(
    model="openai:gpt-5-mini",
    tools=[tool_function],
    system_prompt=SYSTEM_PROMPT,
    context_schema=RuntimeContext
)
```

### Tool Definition

```python
@tool
def execute_sql(query: str) -> str:
    """Execute a SQLite command and return results."""
    runtime = get_runtime(RuntimeContext)
    return runtime.context.db.run(query)
```

### Runtime Context Pattern

```python
@dataclass
class RuntimeContext:
    db: SQLDatabase  # Example from L1
```

## Critical Workflows

### Environment Setup

1. Create and configure `.env`:
   ```
   OPENAI_API_KEY=required
   LANGSMITH_API_KEY=optional
   LANGSMITH_TRACING=true
   ```
2. Install dependencies: `uv sync`
3. Run notebooks: `uv run jupyter lab`

### Debugging Tools

- LangSmith Studio for agent tracing
- Built-in streaming via `agent.stream()`
- Human-in-the-Loop testing (L9_HITL.ipynb)

## Integration Points

### LangSmith Integration

- Set `LANGSMITH_TRACING=true` in `.env`
- Launch studio: `langgraph dev`
- View traces at smith.langchain.com

### MCP (Model Context Protocol)

- Required: Node.js + npx
- See patterns in `L5_tools_with_mcp.ipynb`

## Project Structure

### Core Components

- `L1_fast_agent.ipynb`: Quick-start example
- `L2-L7.ipynb`: Building blocks
- `L8-L9.ipynb`: Advanced customization
- `studio/`: Production-ready examples

### Key Files

- `studio/sql_agent1.py`: Production agent pattern
- `env_utils.py`: Environment validation
- `example.env`: Environment template

## Security Patterns

- SQL query safety in `studio/sql_agent1.py`:
  - Read-only enforcement
  - Query limiting
  - Schema validation

## Notes

- Always configure Python environment before running notebooks
- Use streaming patterns for better UX
- Leverage LangSmith for debugging complex agents
