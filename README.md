Facts Collector
#### Video Demo:  <URL HERE>
Description:
This projects name is called "Facts Collector".
Facts collector has 3 main functions.

Function 1: Search Stock and get Visualization
The “search” page allows users to look up to the latest data of a stock that they would like to look into. When searching for a ticker symbol, it will get a chart of the historic stock price. Users can choose the interval by week, month or year, for example, 2 years or 4 months or 6 weeks of historic stock price. Users also get another 4 categories of data, the basic information, the operation performance, the profitability and the valuation of the company.

Technical
For implementing this function, I used the yahoo finance API for calling my stock data, then used python’s pandas dataframe to store the data, I then convert it to a json format, so that I can pass it to my html file, I then used javascript’s chart.js to display the visual.

For the 4 categories of data, I also used yahoo finance API to get them, so formating to the values had to be done, as well as writing some try-except blocks, since some ticker symbol does not have data for some metrics, for example, ETFs wont have “number of employees”.

Functions 2: Portfolio Simulator
The “portfolio simulator” page allows users to simulate buy and sell stocks, keep track of how the stocks go, and check the net gain of the user. Users could see what stocks they bought, at what price, and since users have to login to do all these actions, their records will  be saved. Hence, users can really try to buy and come back in a year to see how their strategies worked.

Technical:
I used yahoo finance API to get the latest stock price of the stock that the user searched for, and return it as the stock price. Users can choose to buy or sell at that price.
I had a sqlite3 database that stores all the transaction records. The design included a table named “transactions”, whose column names are as follows, “user_id, symbol, quantity, transacted_price_per_share,transaction_type”. A tricky part of the transactions table is that there will be both buy and sell data, hence the “transaction_type” was needed to distinguish the records. When querying for some information, but using some “case when” SQL statements will be sufficient to get any data needed for the application. To save memory for my database, instead of creating a column for “transaction price”, I only store the record of “quantity” and “transacted_price_per_share”, having this two columns and “transaction_type”, while querying data, doing multiplication and combining with case when statements will be sufficient to query almost anything.

To get the “net gain” of users, it requires two parts. On one hand, querying from the database to check what are the stocks that users bought and at what price. On the other side, calling API from yahoo finance to get the latest stock price hence find out the market value of the holdings that users had is also needed. But converting both sides data to a pandas dataframe, then joining them, a single table could be achieved. Plus some calculations on the pandas columns, some additional columns such as ‘% gain’ could also be obtained.


Function 3: Hot News
The hot news function allows users to search for keywords and return what are some hottest news about that keyword to users. It had two types of news provided, stock news and general news. Users are not limited to search for “stocks”, users can also search for “people” and “governments organizations”, such as “Warren Buffet” or “Federal Reserve”.

Technical:
By using web scraping, done with Python libraries requests and BeautifulSoup to send an HTTP request to the Google search page for a given query and retrieve the HTML content of the page. The HTML content is then parsed using BeautifulSoup to extract the relevant information, such as the title, URL, and preview of the search results.
The google_search function takes a query as input and constructs the URL for the Google search using the query parameter. It then sends an HTTP GET request to the constructed URL with a specified User-Agent header to mimic a web browser.
The retrieve_top_results function takes the HTML content of the search results page and the number of results to retrieve. It uses BeautifulSoup to select the relevant HTML elements that contain the desired information, such as the title, URL, and snippet of each search result. It extracts this information and constructs a list of dictionaries representing the top search results.


Overall:
Many functions were written and stored in a file named stock.py, trying to keep the main file as clean as possible.
