# Push users reports
host: api.ocamba.com

Use the /v1/reports/push/users resource to get a custom report. A successful request returns the HTTP 200 OK status code and a JSON or CSV formatted response body. Response body format can be controlled by the HTTP Accept header. By default, this resource returns a CSV formatted response body.


# Dimensions
Dimensions are attributes of your data. 

Value is a string that can take multiple values separated by a comma. 

Maximum length: 100.

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| date_subscribed |string|2021-02-07 15:00:00|The datetime of the subscription.|
| date_unsubscribed |string|2021-02-08 11:33:24|The datetime of the unsubscription.|
| last_touched |string|2021-02-08 11:33:24|The datetime of the last event.|
| user_id |int|1008819|The ID of the user.|
| country_code |string|US|The two-letter country code of the particular country you need data for.|
| country_name |string|United States|Full name of the particular country you need data for.|
| os_id|int|4|The ID of the operating system supported by the Ocamba platform.|
| os_name|string|Mac OS X|The name of the operating system supported by the Ocamba platform.|
| browser_id|int|12|The ID of the browser supported by the Ocamba platform.|
| browser_name|string|Chrome|The name of the browser supported by the Ocamba platform.|
| lang |string|en|The language of the user.|
| source |string|example_source|String used to record and track unique user attributes, traffic sources, banners, and/or link placement.|
| click_id |string|iP3D8CGXUC1LaA6qEbBEQ|| 
| app_id |int|1459574831|The ID of the app.|
| app_name |string|Demo app|The name of the app.|
| app_type |string|web|The app type -> web, android, ios, safari and the default is unknown.|
| extra |string|{"userdata":"example"}|


# Measures
This parameter represents the values that you're measuring. For example, you can measure app performance by looking at your earnings or number of clicks.

Value is a string that can take multiple values separated by a comma.

Maximum length: 100.

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| wokenup |int|15268|The total number of subscribed users.|
| served |int|1277|The total number of served ads.|
| impressions |int|1277|The total number of impressions.|
| clicks |int|1277|The total number of valid clicks.|
| spam_clicks |int|1277|The total number of spam clicks.|
| total_clicks |int|1277|The total number of clicks, including spam clicks.|
| conversions |int|1277|The total number of conversions.|
| income |int|1277|The gain derived from any dimension you requested.|
| cost |int|1277|The cost incurred in the performance of the requested dimension.|

# Other parameters

These parameters are not required. 

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| user_id |int|1008819|This parameter can be used to filter your data by the specific user ID.|
| country_code |string|FR|This parameter can be used to filter your data by the specific country.|
| os_id |int|4|This parameter can be used to filter your data by the specific operating system.|
| browser_id |int|12|This parameter can be used to filter your data by the specific browser.|
| lang |string|en|This parameter can be used to filter your data by the specific user language.|
| source |string|filter_source|This parameter can be used to filter your data by the specific subid/source.|
| app_id |string|1002600|App id created on the Ocamba platform. This parameter can be used to filter your data by the specified app.|
| app_type |string|web|This parameter can be used to filter your data by the app type.|
| sort |string|+delivered|Sort by field. Value should be one of the selected dimensions or measures. "+" represents ascending order, "-" descending.| 
| page |string|2,10|The report can return data paginated by n items. In order to paginate through data, you can specify the “page” query parameter. The default setup is to return the first 100 results.|
| date_subscribed/date_unsubscribed/last_touched |string|2021-02-20 11:00:00|Interval of time.<br>Single Format: Y-m-d<br>Range format: Y-m-d &#124; Y-m-d<br>Hour range format: Y-m-d hh:00:00 &#124; Y-m-d hh:00:00<br>Hour format: Y-m-d hh:00:00<br><br>If “single format” is used, the report displays stats for pixels fired on this specific day.<br>If “range format” is used, the report displays stats for pixels fired in this specific range.<br>If “hour format” is used, the report displays stats for pixels fired in this specific hour.<br><br>For easier search, Reports API gives you the possibility of using one of the following labels:<br><ul><li>today</li><li>yesterday</li><li>last-7-days</li><li>last-30-days</li><li>last-24-hours</li><li>this-month</li><li>last-month</li></ul>|

# Examples
**GET STATISTICS BY DATE SUBSCRIBED(SINGLE FORMAT)**

<pre><code>Sample Request: GET /v1/reports/push/users?dimensions=date_subscribed,user_id, os_name, browser_name&measures=wokenup,impressions,served,clicks,spam_clicks,total_clicks,income,cost&date_subscribed=2021-03-01&sort=-total_clicks

Authorization: Bearer [bearer_token]

Accept: text/csv

Sample Response:

HTTP/1.1 200 OK

date_subscribed,user_id,wokenup,impressions,served,clicks,spam_clicks,total_clicks,income,cost
2021-03-01T11:20:41Z,25160158,2,2,2,1,10,11,0E+00,0E+00
2021-03-01T00:48:37Z,24893358,4,4,4,4,4,8,0E+00,0E+00
2021-03-01T06:12:36Z,25021377,5,5,5,1,5,6,0E+00,0E+00
2021-03-01T05:33:08Z,25006432,3,3,3,2,4,6,0E+00,0E+00
2021-03-01T05:07:40Z,24997184,4,4,4,4,2,6,0E+00,0E+00
2021-03-01T07:59:04Z,25068247,2,2,2,2,3,5,0E+00,0E+00
2021-03-01T06:12:23Z,25021343,4,4,4,4,1,5,0E+00,0E+00
2021-03-01T06:48:23Z,25036224,5,5,5,5,0,5,0E+00,0E+00
2021-03-01T16:09:14Z,25323922,3,3,3,2,3,5,0E+00,0E+00</code></pre>

**GET STATISTICS BY DATE UNSUBSCRIBED (RANGE FORMAT)**

<pre><code>Sample Request: GET /v1/reports/push/users?dimensions=app_name&measures=wokenup,impressions,total_clicks,income&date_unsubscribed=2021-02-20|2021-02-28&sort=-wokenup&app_type=android

Authorization: Bearer [bearer_token]

Accept: text/csv</code></pre>

**GET STATISTICS BY HOUR (HOUR FORMAT)**

<pre><code>Sample Request: GET /v1/reports/push/users?dimensions=country_name&measures=wokenup,impressions,total_clicks,income&last_touched=2021-03-01 15:00:00&sort=-total_clicks

Authorization: Bearer [bearer_token]

Accept: text/csv

Sample Response:

HTTP/1.1 200 OK

country_name,wokenup,impressions,total_clicks,income
Singapore,10,10,8,0E+00
Bangladesh,4,4,8,0E+00
Brazil,8,8,7,0E+00
Japan,6,6,6,0E+00
Brazil,9,8,6,0E+00
Japan,9,8,6,0E+00
United Kingdom,5,4,6,0E+00
Argentina,8,7,6,0E+00
Bangladesh,6,6,5,0E+00</code></pre>

## Report performance (IMPORTANT)

- **A wide date range will increase response time.**
- **It's recommended not to use a date range wider than 30 days.**
- **The number of requested dimensions in the report will have an increasing effect on response time and the amount of data that will be generated by API.**
- **It's recommended to use a lower number of dimensions in reports.**
- **The number of requested measures should not have a significant impact on report performance.**
