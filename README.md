# Stock Screener LLM

An AI-powered stock screener built with **LangGraph**, **Ollama**, and **Yahoo Finance**.

The application allows users to describe the type of stocks or financial assets they are looking for using natural language. A local LLM interprets the request, selects an appropriate Yahoo Finance screener, retrieves market data, and generates a response based on the results.

## How It Works

The application uses a simple LangGraph workflow:

1. The user enters a natural-language request.
2. The request is sent to a local LLM running through Ollama.
3. The LLM decides whether the stock screening tool should be called.
4. The tool selects an appropriate predefined Yahoo Finance screener.
5. Yahoo Finance returns matching assets.
6. The tool extracts relevant market information.
7. The results are passed back to the LLM.
8. The LLM generates the final response for the user.

```text
User Prompt
    │
    ▼
   Ollama
 qwen3.5:9b
    │
    ▼
  LangGraph
    │
    ├──── No tool required ────► Response
    │
    ▼
simple_screener
    │
    ▼
 Yahoo Finance
    │
    ▼
Screener Results
    │
    ▼
    LLM
    │
    ▼
   User
```

## Features

* **Natural-language stock screening** — Search for stocks and other financial assets using normal language.
* **Yahoo Finance integration** — Uses `yfinance` to retrieve screener and market data.
* **LLM tool calling** — The model determines when the stock screening tool should be used.
* **LangGraph workflow** — Coordinates the interaction between the user, LLM, and Yahoo Finance tool.
* **Local LLM** — Uses Ollama with the `qwen3.5:9b` model.
* **Conversation memory** — Uses LangGraph's in-memory checkpointer to maintain context during a session.
* **Paginated screening** — Supports an offset parameter and retrieves five results per tool call.

Supported Yahoo Finance predefined screeners include:

* Aggressive small caps
* Day gainers
* Day losers
* Growth technology stocks
* Most active stocks
* Most shorted stocks
* Small-cap gainers
* Undervalued growth stocks
* Undervalued large caps
* Conservative foreign funds
* High-yield bonds
* Portfolio anchors
* Large-cap growth funds
* Mid-cap growth funds
* Top mutual funds

## Requirements

* Python 3.14+
* [uv](https://docs.astral.sh/uv/)
* [Ollama](https://ollama.com/)
* `qwen3.5:9b` Ollama model

Python dependencies are managed through `pyproject.toml`.

## Installation

Clone the repository:

```bash
git clone https://github.com/AndreiBanu1/stock-screener-llm.git
cd stock-screener-llm
```

Install the project dependencies:

```bash
uv sync
```

Make sure Ollama is installed and running.

Pull the model used by the application:

```bash
ollama pull qwen3.5:9b
```

## Usage

Run the application with:

```bash
uv run python flow.py
```

You will be prompted to enter a request:

```text
🤖 Pass your prompt here:
```

Example prompts:

```text
Show me today's top gainers
```

```text
Find undervalued growth stocks
```

```text
Show me aggressive growth stocks from the technology sector
```

```text
List the most active stocks
```

Press `Ctrl+C` to stop the application.

## Project Structure

```text
.
├── flow.py          # LangGraph workflow, LLM integration, and CLI
├── tool.py          # Yahoo Finance stock screening tool
├── pyproject.toml   # Project metadata and dependencies
├── uv.lock          # Locked dependency versions
└── README.md        # Project documentation
```

### `flow.py`

Defines the LangGraph workflow and connects the application to the local Ollama model.

It is responsible for:

* Initializing `qwen3.5:9b` with `ChatOllama`
* Binding the stock screener as an LLM tool
* Routing between LLM responses and tool execution
* Maintaining conversation state with `InMemorySaver`
* Handling the interactive command-line interface

### `tool.py`

Defines the `simple_screener` LangChain tool.

It is responsible for:

* Receiving a Yahoo Finance screener type
* Receiving an offset for pagination
* Selecting one of Yahoo Finance's predefined screener queries
* Retrieving five matching assets using `yfinance`
* Extracting relevant financial information
* Returning the filtered results to the LLM

The extracted fields can include:

* Symbol
* Company or asset name
* Bid price
* Ask price
* Exchange
* 52-week high
* 52-week low
* Average analyst rating
* Dividend yield

The raw Yahoo Finance screener response is also written to `output.json` during execution for inspection and debugging.

## Example

### Prompt

```text
Return aggressive growth stocks from the technology sector.
```

The LLM interprets the request, selects an appropriate predefined Yahoo Finance screener, retrieves matching assets, and uses the returned market data to generate a response.

Results vary depending on the market data available from Yahoo Finance at the time of the request.

## Development

Ruff is included as a development dependency.

Run the linter with:

```bash
uv run ruff check .
```

To automatically fix supported linting issues:

```bash
uv run ruff check --fix .
```

## Disclaimer

This project is intended for educational and informational purposes only.

Market data provided by Yahoo Finance may be delayed, incomplete, or inaccurate. LLM-generated responses may also contain errors. The output of this application should not be considered financial or investment advice.

## License

This project is licensed under the MIT License.
