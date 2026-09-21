# Stock Screener LLM

A LangGraph-based stock screener that uses Yahoo Finance data to provide financial insights and recommendations.

## Features

- **Yahoo Finance Integration**: Leverages yfinance for real-time stock data
- **LLM-Powered Analysis**: Uses LangChain and Ollama for natural language processing
- **Stock Screening**: Various pre-defined screening criteria including:
  - Day gainers
  - Day losers  
  - Most active stocks
  - Growth technology stocks
  - Undervalued stocks
  - And more...

## Installation

1. Clone the repository
2. Install dependencies using uv:
   ```bash
   uv sync
   ```

## Usage

Run the application:
```bash
python flow.py
```

Then interact with the stock screener by entering prompts like:
- "Show me today's top gainers"
- "Find undervalued growth stocks"
- "List most active stocks"

## Project Structure

```
.
├── flow.py              # Main LangGraph implementation
├── tool.py              # Stock screening tool
├── pyproject.toml       # Project dependencies and configuration
└── README.md            # This file
```

## Dependencies

- langchain>=1.3.15
- langchain-ollama>=1.1.0
- langgraph>=1.2.11
- yfinance>=1.6.0
- colorama>=0.4.6

## License

This project is licensed under the MIT License.