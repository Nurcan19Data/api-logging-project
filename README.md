# api-logging-project
REST API Data Fetching with Error Handling and Logging (Python)

A small Python project that fetches currency exchange rates from a public REST API, handles HTTP errors and network failures, logs every step, and saves the result as a CSV file.

I built this project to practice core API concepts: HTTP requests, JSON responses, status codes, and error logging.

What it does
Sends a GET request to a public exchange rate API (open.er-api.com) using the requests library
Checks the HTTP status code of the response
Retries on temporary failures (5xx errors, timeouts, connection errors) and stops immediately on client errors (4xx)
Validates the response body, because an API can return status 200 and still report an error inside the JSON
Converts the JSON response into a Pandas DataFrame
Saves the result to mezenneler.csv
Writes every request and error to api_layihe.log
Error handling
Situation	Behavior
200 OK	Parse JSON and continue
4xx (client error, e.g. 404)	Log the error and stop, because retrying will not fix a wrong request
5xx (server error)	Log a warning and retry with an increasing delay
Timeout	Log a warning and retry
Connection error	Log a warning and retry
Invalid JSON	Log the error and stop
API returns an error inside a 200 response	Log the error and stop
Tech stack
Python 3
requests
pandas
logging (standard library)
Project structure
.
├── api_layihe.py      # main script
├── requirements.txt   # dependencies
└── README.md
How to run
bash
pip install -r requirements.txt
python api_layihe.py

After running, two files are created:

mezenneler.csv: the exchange rate table
api_layihe.log: request and error log
Testing the error handling

The script includes an xeta_testi() function that sends requests to httpbin.org endpoints that return 404 and 500 on purpose. To try it, uncomment the xeta_testi() line in main() and run the script again, then open api_layihe.log to see how each error is recorded.
