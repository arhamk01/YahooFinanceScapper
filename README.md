# YahooFinanceScapper
Scrapping Yahoo Finance for Historical Stock Prices
Let's go through each function and piece of code in the provided script to understand what it does:

1. **Installing Libraries**: This line installs the necessary libraries (`yfinance` and `pandas`) if they are not already installed.

    ```python
    !pip install yfinance pandas
    ```

2. **Importing Libraries**: Here, the required libraries are imported into the script. `yfinance` is used to fetch stock price data from Yahoo Finance, and `pandas` is used for data manipulation and analysis.

    ```python
    import yfinance as yf
    import pandas as pd
    ```

3. **Setting the Stock Symbol**: Replace `'AAPL'` with the stock symbol of the company you're interested in.

    ```python
    stock_symbol = 'AAPL'
    ```

4. **Fetching Ticker Information**: This part uses the `yfinance.Ticker()` function to get information about the company's stock, like historical data and other details.

    ```python
    ticker = yf.Ticker(stock_symbol)
    ```

5. **Getting Listing Date**: The next line fetches the date when the company was listed on the stock exchange by using the `.history()` method with a `period` argument of `"max"`. The `.index[0]` retrieves the earliest date in the data, which corresponds to the listing date. Likewise you can just put a year like 2010...

    ```python
    start_date = ticker.history(period="max").index[0]
    ```

6. **Fetching Historical Data**: This line retrieves the historical stock price data from the listing date until today with a daily interval. You can modify it to "1mo" for monthly , "1wk" for weekly data or "1d" for daily data, depending on your requirements.

    ```python
    historical_data = ticker.history(start=start_date, end=pd.Timestamp.today(), interval="1d")
    ```

7. **Removing Timezone Information**: To address the issue of Excel not supporting timezones, this line removes timezone information from the datetime index.

    ```python
    historical_data.index = historical_data.index.tz_localize(None)
    ```

8. **Exporting to Excel**: This code exports the historical stock price data to an Excel file named "---.xlsx" and saves it in the `/content` directory of the Colab environment. You can change your name here.

    ```python
    excel_filename = "/content/---.xlsx"
    historical_data.to_excel(excel_filename, engine='openpyxl')
    ```

9. **Printing Confirmation**: This line prints a message indicating that the data has been successfully exported.

    ```python
    print(f"Data exported to {excel_filename}")
    ```

The script fetches historical stock price data for the specified stock symbol from Yahoo Finance, removes timezone information from the datetime index, and then exports the data to an Excel file named "stockprice.xlsx" in the Colab environment's `/content` directory. Make sure to adjust the stock symbol and file paths as needed.
