### Get company's financial data from Yahoo Finance as Pandas Dataframe

***

#### Rationale:

- Off the shelf libraries such as [yfinance](https://github.com/ranaroussi/yfinance/) and [yahoofinancials](https://github.com/JECSand/yahoofinancials) are great
- However, there appears to be a problem with the yahoo api (or maybe me)
  - [Financials retrieved very different from the Yahoo Finance site](https://github.com/JECSand/yahoofinancials/issues/102)
  - [`.balancesheet` method does not have 'Total Debt' like Yahoo Finance](https://github.com/ranaroussi/yfinance/issues/895)
- When checking the api returns for the website, it seems that it returns a version with completely different naming conventions

#### Idea:

- Use Selenium to launch a browser for button click functionality (if needed; such as for expanding of table rows)
- Gets the data and converts them to dataframe after cleaning up

#### possible improvements

- Currently, if yahoo decides to update their website interface, this code is in trouble. 
- current method requires launching a (headless) browser, and open a tab which slows down the program. Takes up to ~15 seconds for longer queries
  - well, if it's too fast, that would open the potential for misuse? 

#### Troubleshooting

Sometimes, after installing a package, it may not appear on jupyter as its not added to path.

Get the path to your conda (`python -m site`) or python path where site-packages are stored. Then run, 

```
import sys
sys.path.append(path_to_your_site_packages)
```

#### Reference:

Run the cells in order.

```python
def get_financial_data(ticker, statement_type, expanded=False, quarterly=False):
```

1. `ticker` - Name of company in letters on finance yahoo
2. `statement_type` 
   - 'CF' for Cash Flow
   - 'BS' for Balance Sheet
   - 'INC' for Income Statement
3. `expanded` (defaults to false)
   - On Yahoo Finance there is an option to increase the number of rows with more financial data
4. `quarterly` (defaults to false)
   - If set to false, will get yearly data based on what you can see on Yahoo Finance


To get a specific row, we can use use [pandas Dataframe methods!](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html)

```python
df.loc[[row_name]]
```

For getting a specific value, indexed by row and column name

```python
df.at[row_name, col_name]
```

