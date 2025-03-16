# S&P 500 Financial Calendar Tracker

This Python script fetches financial calendar data (earnings, dividends, revenue) for S&P 500 companies using the `yfinance` library, highlights important events, and sends WhatsApp notifications via Twilio. It’s designed to run in Google Colab but can be adapted for local execution.

## Features
- **Data Collection**: Scrapes S&P 500 tickers from Wikipedia and retrieves financial data via Yahoo Finance.
- **Event Highlighting**: Identifies key events like upcoming earnings (within 7 days) and significant dividends (e.g., >$0.03).
- **Notifications**: Sends alerts to your WhatsApp number using Twilio.
- **Output**: Displays results in Colab and provides a downloadable CSV file.

## Prerequisites
1. **Python Libraries**:
   - `yfinance`: For financial data.
   - `pandas`: For data manipulation.
   - `twilio`: For WhatsApp notifications.
   - `requests`: For web scraping.
   Install them in Colab with:
   ```bash
   !pip install yfinance pandas twilio requests
   ```
   Or locally with:
   ```bash
   pip install yfinance pandas twilio requests
   ```

2. **Twilio Account**:
   - Sign up at [Twilio](https://www.twilio.com/).
   - Get your `ACCOUNT_SID`, `AUTH_TOKEN`, and a Twilio phone number with WhatsApp enabled (sandbox available for testing).
   - Register your WhatsApp number with the sandbox by texting "join <sandbox-keyword>" to the Twilio number.

3. **Google Colab** (optional):
   - If running in Colab, no local setup is needed beyond the script.

## Setup
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/sp500-financial-calendar.git
   cd sp500-financial-calendar
   ```

2. **Configure Twilio Credentials**:
   - Open `sp500_tracker.py` (or your Colab notebook).
   - Replace the placeholders:
     ```python
     ACCOUNT_SID = "YOUR_TWILIO_ACCOUNT_SID"
     AUTH_TOKEN = "YOUR_TWILIO_AUTH_TOKEN"
     YOUR_WHATSAPP_NUMBER = "whatsapp:+12345678901"  # Your number in international format
     ```

3. **Run in Colab**:
   - Upload `sp500_tracker.py` to Colab or copy-paste into a notebook cell.
   - Execute the cell to install dependencies and run the script.

4. **Run Locally** (optional):
   - Install dependencies (see above).
   - Run the script:
     ```bash
     python sp500_tracker.py
     ```

## Usage
- **Script Execution**:
  - Fetches S&P 500 tickers and financial data for the next 7 days (configurable via `days_ahead`).
  - Limits to 10 tickers by default for testing (edit `tickers[:10]` to process all 500).
  - Sends WhatsApp notifications for important events.
  - In Colab, displays DataFrames and downloads a CSV file (`sp500_financial_calendar.csv`).

- **Customization**:
  - Adjust the `highlight_important_events` function to change what qualifies as "important" (e.g., dividend threshold).
  - Modify `days_ahead` in `get_financial_calendar` for a different time window.

## Example Output
WhatsApp message:
```
Important Event Alert!
Ticker: AAPL
Event: Earnings
Date: 2025-03-20
Details: Earnings Report
```

CSV file (`sp500_financial_calendar.csv`):
```
Ticker,Event,Date,Details
AAPL,Earnings,2025-03-20,Earnings Report
MSFT,Dividend,2025-03-18,Dividend: $0.75
GOOGL,Revenue,2025-03-16,Revenue: $85.32B
```

## Limitations
- **API Reliability**: `yfinance` is unofficial and may miss future calendar events or have inconsistent data.
- **Rate Limits**: Yahoo Finance and Twilio have limits; the script includes delays (`time.sleep()`) to mitigate this.
- **Scope**: Revenue data is retrospective (latest reported), not scheduled.
- **Colab Runtime**: Processing all 500 tickers may timeout in Colab; consider batching or a premium API.

## Future Improvements
- Integrate a premium API (e.g., Alpha Vantage, Polygon.io) for better data accuracy.
- Add scheduling (e.g., via Google Cloud Scheduler) for daily updates.
- Enhance event filtering with user-defined criteria.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing
Feel free to fork this repository, submit pull requests, or open issues for bugs and feature requests!

---
