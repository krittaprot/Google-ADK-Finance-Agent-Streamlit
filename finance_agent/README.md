# Financial Agent with YFinance Tools

Adapted from: https://docs.agno.com/examples/agents/finance-agent

A powerful financial analysis assistant built with Google ADK (Agent Development Kit) and integrated with YFinance for real-time market data.

## Features

🔍 **Real-time Stock Data**
- Current stock prices with currency information
- Live market data during trading hours

📊 **Company Analysis**
- Comprehensive company profiles and business information
- Key financial metrics and ratios
- Market capitalization and trading statistics

📈 **Historical Data**
- Historical stock prices with customizable time periods
- Support for different data intervals (daily, weekly, monthly)
- Trend analysis capabilities

💰 **Financial Fundamentals**
- P/E ratios, EPS, and other key metrics
- Debt-to-equity ratios and profitability margins
- Return on equity and assets analysis
- Income statement analysis
- Key financial ratios
- Analyst recommendations
- Technical indicator analysis

📰 **Market News**
- Latest company news and press releases
- Market developments and announcements
- Configurable number of news stories

🌐 **Web Search**
- Real-time web search for general financial news and information
- Access to a broader range of financial topics beyond specific stock data

## Setup

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Environment Configuration

Create a `.env` file in the project root with your OpenRouter and Tavily API credentials:

```env
OPENROUTER_API_KEY=your_openrouter_api_key_here
OPENROUTER_BASE_URL=https://openrouter.ai/api/v1
TAVILY_API_KEY=your_tavily_api_key_here
```

### 3. Verify Installation

Test that yfinance is working:

```python
import yfinance as yf
stock = yf.Ticker("AAPL")
print(stock.info.get("regularMarketPrice"))
```

## Usage

### Basic Usage

You can interact with the financial agent using the ADK CLI for terminal-based conversations or the ADK web UI for a browser-based experience.

#### Run in Terminal

To run the agent in your terminal:

```bash
adk run finance_agent
```

You can then type your queries directly in the terminal. To exit, use `Ctrl+C`.

#### Run in Web UI

To launch the interactive developer UI in your browser:

```bash
adk web
```

Open your browser to `http://localhost:8000` (or the URL provided). In the top-left corner, select your agent (`finance_agent` if you renamed the directory, or the default `agent` name if not explicitly changed) from the dropdown. You can then chat with the agent through the web interface.

### Available Tools

The financial agent has access to these YFinance and Tavily tools:

#### `get_current_stock_price(symbol: str)`
Get real-time stock price for any symbol.

**Example:** "What's the current price of Tesla stock?"

#### `get_company_info(symbol: str)`
Get comprehensive company information including business summary, financials, and key metrics.

**Example:** "Tell me about Microsoft as a company"

#### `get_historical_stock_prices(symbol: str, period: str, interval: str)`
Get historical price data with customizable periods and intervals.

**Example:** "Show me Apple's stock performance over the last year"

#### `get_stock_fundamentals(symbol: str)`
Get key financial ratios and fundamental analysis data.

**Example:** "What are Google's financial fundamentals?"

#### `get_company_news(symbol: str, num_stories: int)`
Get recent news and press releases for a company.

**Example:** "What's the latest news about Amazon?"

#### `get_income_statements(symbol: str)`
Get income statements for a given stock symbol.

**Example:** "Show me the income statement for Google (GOOGL)"

#### `get_key_financial_ratios(symbol: str)`
Get key financial ratios for a given stock symbol.

**Example:** "What are the key financial ratios for Microsoft (MSFT)?"

#### `get_analyst_recommendations(symbol: str)`
Get analyst recommendations for a given stock symbol.

**Example:** "What are the analyst recommendations for Apple (AAPL)?"

#### `get_technical_indicators(symbol: str, period: str)`
Get technical indicators for a given stock symbol with customizable periods.

**Example:** "Show me the technical indicators for Tesla (TSLA) over the last 3 months"

#### `tavily_search_results(query: str, max_results: int, search_depth: str, include_answer: bool, include_raw_content: bool, include_images: bool, time_range: str, topic: str)`
Perform a comprehensive web search using Tavily.

**Example:** "What are the latest financial news headlines for Google?"

### Example Queries

Here are some example queries you can try:

1.  **Stock Prices**
    - "What's the current stock price of Apple (AAPL)?"
    - "How is Tesla (TSLA) performing today?"

2.  **Company Analysis**
    - "Give me detailed information about Microsoft (MSFT)"
    - "What sector is Amazon (AMZN) in and what do they do?"

3.  **Historical Data**
    - "Show me Google's (GOOGL) stock performance over the last 6 months"
    - "What was the historical trend for Netflix (NFLX) in 2023?"

4.  **Financial Fundamentals**
    - "What are the key financial ratios for Apple (AAPL)?"
    - "How profitable is Microsoft (MSFT) based on its fundamentals?"

5.  **Income Statements**
    - "Get the income statement for Amazon (AMZN)."
    - "Can you provide the income statement for Netflix (NFLX)?"

6.  **Key Financial Ratios**
    - "What are the key financial ratios for Google (GOOGL)?"
    - "Show me the key financial ratios for Tesla (TSLA)."

7.  **Analyst Recommendations**
    - "What are the latest analyst recommendations for Microsoft (MSFT)?"
    - "Are there any analyst recommendations for Apple (AAPL)?"

8.  **Technical Indicators**
    - "Show me the technical indicators for Nvidia (NVDA) for the last 6 months."
    - "What are the technical indicators for AMD (AMD)?"

9.  **Market News**
    - "What's the latest news about Tesla (TSLA)?"
    - "Are there any recent developments with Amazon (AMZN)?"

10. **General Financial Search**
    - "What are the latest economic indicators for the US market?"
    - "Summarize recent news about inflation and its impact on the stock market."

### Supported Stock Symbols

The agent works with any valid stock symbol supported by Yahoo Finance, including:

-   **US Stocks**: AAPL, GOOGL, MSFT, TSLA, AMZN, META, NVDA, etc.
-   **International Stocks**: Use appropriate suffixes (e.g., ASML.AS for European stocks)
-   **ETFs**: SPY, QQQ, VTI, etc.
-   **Indices**: ^GSPC (S&P 500), ^IXIC (NASDAQ), etc.

### Deploy as Local API

You can also run your ADK agent as a local API server, allowing for programmatic interaction. This is useful for integrating your agent into other applications or for advanced testing.

#### Run the API Server

Navigate to the `parent_folder` directory in your terminal and run the following command:

```bash
parent_folder/
└── my_sample_agent/
    └── agent.py (or Agent.java)
```

Launch the server

```bash
adk api_server --host 0.0.0.0 --port 8000
```

This will start a local web server, typically on `http://localhost:8000`. You should see output similar to:

```
INFO:     Started server process [PID]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://localhost:8000 (Press CTRL+C to quit)
```

#### Interact with the API

Once the API server is running, you can interact with your agent using `curl` commands (or any other HTTP client).

1.  **Create a new session:**

    You can create a new session for your agent. Replace `finance_agent` with your actual agent's directory name if different, and `u_123`, `s_123` with your desired user and session IDs.

    ```bash
    curl -X POST http://localhost:8000/apps/finance_agent/users/u_123/sessions/s_123 \
      -H "Content-Type: application/json" \
      -d '{"state": {}}'
    ```

    (The `state` object is optional and can be used to set initial session state.)

2.  **Send a query to the agent:**

    You can use either the `/run` (returns all events at once) or `/run_sse` (returns Server-Sent Events for streaming) endpoints.

    **Using `/run` (recommended for most users):**

    ```bash
    curl -X POST http://localhost:8000/run \
    -H "Content-Type: application/json" \
    -d '{
    "appName": "finance_agent",
    "userId": "u_123",
    "sessionId": "s_123",
    "newMessage": {
        "role": "user",
        "parts": [{
        "text": "What is the current stock price of Apple (AAPL)?"
        }]
    }
    }'
    ```

    **Using `/run_sse` (for streaming responses):**

    ```bash
    curl -X POST http://localhost:8000/run_sse \
    -H "Content-Type: application/json" \
    -d '{
    "appName": "finance_agent",
    "userId": "u_123",
    "sessionId": "s_123",
    "newMessage": {
        "role": "user",
        "parts": [{
        "text": "What is the current stock price of Apple (AAPL)?"
        }]
    },
"streaming": true
}'
    ```

    Set `"streaming": true` to enable token-level streaming.

    The API will return a JSON object containing the agent's response, including any tool calls and final answers.

## Limitations

-   Data is sourced from Yahoo Finance and subject to their terms of service
-   Real-time data may have slight delays
-   Some international stocks may have limited data availability
-   This tool is for educational and research purposes only - not investment advice

## Contributing

Feel free to extend the agent with additional financial tools or improve existing functionality. The modular design makes it easy to add new YFinance capabilities.

## License

This project is for educational purposes. Please respect Yahoo Finance's terms of service when using their data.

---

**Disclaimer**: This financial agent is for educational and informational purposes only. It does not constitute financial advice. Always consult with qualified financial professionals before making investment decisions.
