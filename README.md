# Stock Screener LLM

A LangGraph-based stock screening application that combines Yahoo Finance market data with an LLM to help users discover and analyze stocks using natural-language queries.

## Features

* **Yahoo Finance Integration** — Retrieves stock market and financial data using `yfinance`.
* **LLM-Powered Queries** — Uses LangChain and Ollama to interpret natural-language screening requests.
* **LangGraph Workflow** — Coordinates the interaction between the LLM and stock screening tools.
* **Predefined Stock Screeners** — Supports several screening strategies, including:

  * Day gainers
  * Day losers
  * Most active stocks
  * Growth technology stocks
  * Undervalued stocks
  * And more

## Installation

Clone the repository and install the project dependencies using `uv`:

```bash
uv sync
```

Make sure Ollama is installed and running before starting the application.

## Usage

Run the application with:

```bash
python flow.py
```

You can then enter natural-language queries such as:

```text
Show me today's top gainers
```

```text
Find undervalued growth stocks
```

```text
List the most active stocks
```

## Project Structure

```text
.
├── flow.py          # Main LangGraph workflow
├── tool.py          # Stock screening tools
├── pyproject.toml   # Project dependencies and configuration
└── README.md        # Project documentation
```

## Dependencies

* `langchain>=1.3.15`
* `langchain-ollama>=1.1.0`
* `langgraph>=1.2.11`
* `yfinance>=1.6.0`
* `colorama>=0.4.6`

## Example

### Prompt

```text
Return a list of aggressive growth stocks from the technology sector.
```

### Response

The application returns matching stocks together with relevant Yahoo Finance data, such as:

```json
{
  "start": 0,
  "count": 5,
  "total": 57,
  "quotes": [
    {
      "symbol": "WDC",
      "shortName": "Western Digital Corporation",
      "regularMarketPrice": 441.36,
      "regularMarketChangePercent": 4.126263,
      "marketCap": 159128338432,
      "trailingPE": 16.395245,
      "forwardPE": 13.901307,
      "fiftyTwoWeekChangePercent": 292.6341
    }
  ]
}
```

The exact fields and results depend on the selected screener and the market data returned by Yahoo Finance.

## Disclaimer

This project is intended for educational and informational purposes only. Market data may be delayed or incomplete, and the output should not be considered financial or investment advice.

## License

This project is licensed under the MIT License.
