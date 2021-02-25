# Push stats reports
host: api.ocamba.com

Use the /v1/reports/push/stats resource to get a custom report. A successful request returns the HTTP 200 OK status code and a JSON or CSV formatted response body. Response body format can be controlled by the HTTP Accept header. By default, this resource returns a CSV formatted response body.


# Dimensions
Dimensions are attributes of your data. 

Value is a string that can take multiple values separated by a comma. 

Maximum length: 100.

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| [stat_date](#stat_date_anchor) |string|2021-02-07 15:00:00|Event datetime.|
| app_id |int|1459574831|The ID of the app.|
| app_name |string|Demo app|The name of the app.|
| country_code |string|US|The two-letter country code of the particular country you need data for.|
| country_name |string|United States|Full name of the particular country you need data for.|
| source |string|example_source|String used to record and track unique user attributes, traffic sources, banners, and/or link placement.|
| lang |string|en|The language of the user.|
| app_type |string|web|The app type -> web, android, ios, safari and the default is unknown.|
| os_id|int|4|The ID of the operating system supported by the Ocamba platform.|
| os_name|string|Mac OS X|The name of the operating system supported by the Ocamba platform.|
| browser_id|int|12|The ID of the browser supported by the Ocamba platform.|
| browser_name|string|Chrome|The name of the browser supported by the Ocamba platform.|

# Measures
This parameter represents the values that you're measuring. For example, you can measure app performance by looking at your earnings or number of clicks.

Value is a string that can take multiple values separated by a comma.

Maximum length: 100.

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| subscribed |int|15268|The total number of subscribed users.|
| unsubscribed |int|1277|The total number of unsubscribed users.|

# Other parameters

These parameters are not required. 

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| app_id |string|1002600|App id created on the Ocamba platform. This parameter can be used to filter your data by the specified app.|
| country_code |string|FR|This parameter can be used to filter your data by the specific country.|
| source |string|filter_source|This parameter can be used to filter your data by the specific subid/source.|
| lang |string|en|This parameter can be used to filter your data by the specific user language.|
| app_type |string|android|This parameter can be used to filter your data by the specific app type.|
| os_id |int|4|This parameter can be used to filter your data by the specific operating system.|
| browser_id |int|12|This parameter can be used to filter your data by the specific browser.|
| sort |string|+delivered|Sort by field. Value should be one of the selected dimensions or measures. "+" represents ascending order, "-" descending.| 
| page |string|2,10|The report can return data paginated by n items. In order to paginate through data, you can specify the “page” query parameter. The default setup is to return the first 100 results.<a name="stat_date_anchor"></a>|
| stat_date |string|2020-12-08|Interval of time.<br>Single Format: Y-m-d<br>Range format: Y-m-d &#124; Y-m-d<br>Hour range format: Y-m-d hh:00:00 &#124; Y-m-d hh:00:00<br>Hour format: Y-m-d hh:00:00<br><br>If “single format” is used, the report displays stats for this specific day by hours.<br>If “range format” is used, the report displays stats in this specific range by hours.<br>If “hour format” is used, the report displays stats in this specific hour.<br><br>If you exclude this parameter, the default setup displays "today" stats.<br><br>For easier search, Reports API gives you the possibility of using one of the following labels:<br><ul><li>today</li><li>yesterday</li><li>last-7-days</li><li>last-30-days</li><li>last-24-hours</li><li>this-month</li><li>last-month</li><li>infinity</ul><br>When getting summary statistics it is needed to use the infinity label. In that case, you can not request hourly/daily breakdown by adding the stat_date in the dimensions parameter.|

# Examples
**GET STATISTICS BY DATE (SINGLE FORMAT)**

<pre><code>Sample Request: GET /v1/reports/push/stats?stat_date=2021-02-07&dimensions=app_id,app_name&measures=subscribed,unsubscribed

Authorization: Bearer [bearer_token]

Accept: text/csv

Sample Response:

HTTP/1.1 200 OK

Content-Type: text/csv</code></pre>

**GET STATISTICS BY DATE RANGE (RANGE FORMAT)**

<pre><code>Sample Request: GET /v1/reports/push/stats?stat_date=2021-02-05|2021-02-07&dimensions=os_id,os_name&measures=subscribed,unsubscribed

Authorization: Bearer [bearer_token]

Accept: text/csv</code></pre>

**GET STATISTICS BY HOUR (HOUR FORMAT)**

<pre><code>Sample Request: GET /v1/reports/push/stats?stat_date=2021-02-06 15:00:00&dimensions=browser_id,browser_name&measures=subscribed,unsubscribed

Authorization: Bearer [bearer_token]

Accept: text/csv</code></pre>

**GET TOP TEN BROWSERS BY NUMBER OF SUBSCRIBED USERS<br>**
**FOR THE LAST MONTH FILTERED BY OS**

<pre><code>Sample Request: GET /v1/reports/push/stats?dimensions=browser_name&measures=subscribed&os_id=12&stat_date=last-month&page=1,10&sort=-subscribed

Authorization: Bearer [bearer_token]

Accept: text/csv</code></pre>

**GET TOP FIVE COUNTRIES BY THE NUMBER OF SUBSCRIBED USERS FOR THE SPECIFIC HOUR**

<pre><code>Sample Request: GET /v1/reports/push/stats?dimensions=country_name&measures=subscribed&stat_date=2021-02-07 12:00:00&page=1,5&sort=-subscribed

Authorization: Bearer [bearer_token]

Accept: text/csv</code></pre>

**GET TOP TEN APPS BY THE NUMBER OF UNSUBSCRIBED USERS**

<pre><code>Sample Request: GET /v1/reports/push/stats?dimensions=app_name&measures=unsubscribed&page=1,10&sort=-unsubscribed

Authorization: Bearer [bearer_token]

Accept: text/csv</code></pre>

## Report performance (IMPORTANT)

- **A wide date range will increase response time.**
- **It's recommended not to use a date range wider than 30 days.**
- **The number of requested dimensions in the report will have an increasing effect on response time and the amount of data that will be generated by API.**
- **It's recommended to use a lower number of dimensions in reports.**
- **The number of requested measures should not have a significant impact on report performance.**
