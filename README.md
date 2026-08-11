# MULTI-AI-AGENT-SYSTEM-

A multi-agent research and tooling framework that composes search, scraping, writing, and critique agents to run automated research pipelines.

## Features

- Search the web for recent, reliable information.
- Scrape and extract readable content from web pages.
- Draft structured research reports from gathered data.
- Run a critic chain to evaluate and give feedback on reports.

## Quick Start

1. Clone the repository:

```bash
git clone <repo_url>
cd MULTI-AI-AGENT-SYSTEM-
```

2. Create and activate a Python environment (recommended: conda):

```bash
conda create -n langagent python=3.11 -y
conda activate langagent
pip install -r requirements.txt
```

3. Configure environment variables (create a `.env` file):

```
GROQ_API_KEY=your_groq_api_key
TAVILY_API_KEY=your_tavily_api_key
```

4. Run the example:

```bash
python main.py
```

## Technologies Used

- Python 3.11+
- LangChain (agents, chains, tools)
- langchain_groq / ChatGroq (GROQ-backed LLM client)
- tavily (web search API)
- requests, BeautifulSoup, trafilatura, readability (web scraping and content extraction)
- dotenv (environment variable loading)

## Project Structure

- `main.py` — simple entrypoint example that runs the research pipeline.
- `app.py` — (optional) Streamlit or web UI runner (if present).
- `SRC/AGENTS/AGENTS.py` — definitions for building the LLM agents and chains (search agent, scrape/reader agent, writer chain, critic chain).
- `SRC/PIPELINES/PIPELINES.py` — orchestration pipeline that composes agents to perform multi-step research.
- `SRC/TOOLS/Tools.py` — tool wrappers for web search and scraping, exposed as LangChain tools.

## Architecture (Brief)

The system follows a pipeline architecture composed of independent agents and tools:

- Tools layer: low-level utilities that perform web search and scraping (`SRC/TOOLS/Tools.py`). These are wrapped with LangChain `tool` decorators to present a uniform interface.
- Agent layer: LLM-backed agents and chains built in `SRC/AGENTS/AGENTS.py`. Agents call tools and chains to produce structured outputs (search results, scraped text, reports, and critiques).
- Pipeline/orchestration layer: `SRC/PIPELINES/PIPELINES.py` sequences the work: search → scrape → write → critique, maintaining a `state` object with intermediate results.
- Entry points: `main.py` demonstrates running the pipeline; `app.py` (if used) can provide a UI around the pipeline.

This separation keeps responsibilities clear and makes it easy to swap tools or LLM backends.

## Configuration

- Add API keys to `.env` as shown above. The project expects `GROQ_API_KEY` and `TAVILY_API_KEY`.
- Adjust LLM settings in `SRC/AGENTS/AGENTS.py` (model name, temperature).

## Development

- Run unit tests (if added) and format code with `black` / `ruff` as needed.
- Open an interactive REPL and import modules for iterative development.

## Contributing

Contributions welcome. Please open issues or PRs with clear descriptions and tests when appropriate.

## License

See the `LICENSE` file in the repository root.
