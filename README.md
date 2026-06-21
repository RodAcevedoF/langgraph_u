# langgraph_u

Course notebooks for building agents with **LangChain 1.x** and **LangGraph**, organized by chapter.

## Setup

Requires [uv](https://docs.astral.sh/uv/) and Python 3.13 (pinned via `.python-version`).

```bash
uv sync                       # create .venv and install dependencies
cp .env.example .env          # then fill in your API keys
uv run jupyter lab            # launch JupyterLab from this directory
```

Run all `uv` / `jupyter` commands from inside `langgraph_u/`.

### Environment variables

Copy `.env.example` to `.env` and set:

| Variable | Purpose |
|---|---|
| `OPENAI_API_KEY` | OpenAI (or Vocareum proxy) API key |
| `OPENAI_BASE_URL` | API base URL (e.g. the Vocareum proxy endpoint) |
| `TAVILY_API_KEY` | Tavily search (used by the tool-calling / API notebooks) |

`.env` is git-ignored — never commit your keys.

## Structure

| Chapter | Topics |
|---|---|
| `01_agents/` | Agents from scratch, self-reflection & memory, tool calling, multi-agents |
| `02_workflows/` | The Agent class, multi-step workflows, building a graph from scratch |
| `03_state_routing/` | Reducers, limiting messages, routers, the loan agent |
| `04_rag_memory_obs/` | Calling APIs, persisting memory, embeddings, ChromaDB, LangMem, human-in-the-loop, observability, the KB agent, evaluation |

Notebooks are named `demo_NN_topic` / `exercise_NN_topic` (plus a few `*_from_scratch` explorations), and each opens with a descriptive `#` heading.

## Notes

- **ragas evaluation is disabled** in `04_rag_memory_obs/exercise_02_evaluation.ipynb`. The latest ragas imports `langchain_community.chat_models.vertexai`, a module removed in langchain-community 0.4.x, so `import ragas` crashes on this modern stack. The cell is commented out with details on how to restore it.
- The **KB agent** and **evaluation** notebooks load `compact-guide-to-large-language-models.pdf`, which is **not included** — add it to `04_rag_memory_obs/` to run them.
- The **observability** notebook expects an MLflow server at `http://127.0.0.1:5000`. Start one from this directory:
  ```bash
  uv run mlflow server --backend-store-uri sqlite:///mlflow.db
  ```
- Generated stores (`*.db`, `chromadb/`) are git-ignored and recreated when you run the notebooks.
