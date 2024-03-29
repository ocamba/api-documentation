# Push users reports
host: api.ocamba.com

Use the /v1/reports/push/users resource to get a custom report. A successful request returns the HTTP 200 OK status code and a JSON or CSV formatted response body. Response body format can be controlled by the HTTP Accept header. By default, this resource returns a CSV formatted response body.


# Dimensions
Dimensions are attributes of your data. 

Value is a string that can take multiple values separated by a comma. 

Maximum length: 100.

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| date_subscribed |string|2021-02-07 15:00:00|The DateTime of the subscription.|
| date_unsubscribed |string|2021-02-08 11:33:24|The DateTime of the unsubscription.|
| last_touched |string|2021-02-08 11:33:24|The DateTime of the last event.|
| user_id |int|1008819|The ID of the user.|
| country_code |string|US|The two-letter country code of the particular country you need data for.|
| country_name |string|United States|Full name of the particular country you need data for.|
| os_id|int|4|The ID of the operating system supported by the Ocamba platform.|
| os_name|string|Mac OS X|The name of the operating system supported by the Ocamba platform.|
| browser_id|int|12|The ID of the browser supported by the Ocamba platform.|
| browser_name|string|Chrome|The name of the browser supported by the Ocamba platform.|
| lang |string|en|The language of the user.|
| source |string|example_source|String used to record and track unique user attributes, traffic sources, banners, and/or link placement.|
| app_id |int|1459574831|The ID of the app.|
| app_name |string|Demo app|The name of the app.|
| app_type |string|web|The app type. Values can be web, android, ios, and the default is unknown.|
| conn_type |string|cable/dsl|The type of the connection supported by Ocamba.|
| conn_type_id |int|4|The ID of the connection type. (1 - 'dialup', 2 - 'cable/dsl', 3 - 'corporate', 4 - 'cellular')|
| asn |int|15169|The Autonomous System Number supported by Ocamba.|
| isp |string|Google|Internet Service Provider supported by Ocamba.|
| city_name |string|Sydney|The name of the city supported by Ocamba.|
| city_id |int|6354908|The GeoName ID of the city supported by Ocamba.|
| status |string|subscribed|The status of user. ('subscribed', 'unsubscribed', 'inactive')|
| extra |string|{"userdata":"example"}|Additional information of the user providing you with better insight into the user behavior and preferences.|


# Measures
This parameter represents the values that you're measuring. For example, you can measure app performance by looking at your earnings or number of clicks.

Value is a string that can take multiple values separated by a comma.

Maximum length: 100.

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| wokenup |int|15268|The total number of woken users.|
| served |int|1277|The total number of served ads.|
| impressions |int|2265432|The total number of impressions.|
| clicks |int|33615|The total number of valid clicks.|
| spam_clicks |int|535|The total number of spam clicks.|
| total_clicks |int|34150|The total number of clicks, including spam clicks.|
| conversions |int|64|The total number of conversions.|
| income |int|3304.45|The gain derived from any dimension you requested.|
| cost |int|126.32|The cost incurred in the performance of the requested dimension.|

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
| clicker |string|neq:0|This parameter is used to filter your data by the user data "clicker". Allowed operations are equal and not equal. If you want to get users which are already defined as clicker/non clicker, you should only pass the value to the parameter, ex "&clicker=0". If you want to exclude these users in search, you should use not equal operator, ex "&clicker=neq:0".
| sort |string|+delivered|Sort by field. Value should be one of the selected dimensions or measures. "+" represents ascending order, "-" descending.| 
| page |string|2,10|The report can return data paginated by n items. In order to paginate through data, you can specify the “page” query parameter. The default setup is to return the first 100 results.|
| status |string|active|This parameter is used if you want to get only active users.|
| date_subscribed |string|2021-02-20 11:00:00|Interval of time.<br>Single Format: Y-m-d<br>Range format: Y-m-d &#124; Y-m-d<br>Hour range format: Y-m-d hh:00:00 &#124; Y-m-d hh:00:00<br>Hour format: Y-m-d hh:00:00<br><br>If “single format” is used, the report displays stats for users subscribed on this specific day.<br>If “range format” is used, the report displays stats for users subscribed in this specific range.<br>If “hour format” is used, the report displays stats for users subscribed in this specific hour.<br><br>For easier search, Reports API gives you the possibility of using one of the following labels:<br><ul><li>today</li><li>yesterday</li><li>last-7-days</li><li>last-30-days</li><li>last-24-hours</li><li>this-month</li><li>last-month</li></ul>|
| date_unsubscribed |string|2021-02-20 11:00:00|Interval of time.<br>Single Format: Y-m-d<br>Range format: Y-m-d &#124; Y-m-d<br>Hour range format: Y-m-d hh:00:00 &#124; Y-m-d hh:00:00<br>Hour format: Y-m-d hh:00:00<br><br>If “single format” is used, the report displays stats for users unsubscribed on this specific day.<br>If “range format” is used, the report displays stats for users unsubscribed in this specific range.<br>If “hour format” is used, the report displays stats for users unsubscribed in this specific hour.<br><br>For easier search, Reports API gives you the possibility of using one of the following labels:<br><ul><li>today</li><li>yesterday</li><li>last-7-days</li><li>last-30-days</li><li>last-24-hours</li><li>this-month</li><li>last-month</li></ul>|
| last_touched |string|2021-02-20 11:00:00|Interval of time.<br>Single Format: Y-m-d<br>Range format: Y-m-d &#124; Y-m-d<br>Hour range format: Y-m-d hh:00:00 &#124; Y-m-d hh:00:00<br>Hour format: Y-m-d hh:00:00<br><br>If “single format” is used, the report displays stats for users which last time had any activity on this specific day.<br>If “range format” is used, the report displays stats for users subscribed in this specific range.<br>If “hour format” is used, the report displays stats for users subscribed in this specific hour.<br><br>For easier search, Reports API gives you the possibility of using one of the following labels:<br><ul><li>today</li><li>yesterday</li><li>last-7-days</li><li>last-30-days</li><li>last-24-hours</li><li>this-month</li><li>last-month</li></ul>|

# Examples
**GET STATISTICS BY DATE SUBSCRIBED(SINGLE FORMAT)**

<pre><code>Sample Request: GET /v1/reports/push/users?dimensions=date_subscribed,user_id,os_name,browser_name&measures=wokenup,impressions,served,clicks,spam_clicks,total_clicks,income,cost&date_subscribed=2021-03-01&sort=-total_clicks

Authorization: Bearer [bearer_token]

Accept: text/csv

Sample Response:

HTTP/1.1 200 OK

date_subscribed,user_id,os_name,browser_name,wokenup,impressions,served,clicks,spam_clicks,total_clicks,income,cost
2021-03-01T11:20:41Z,25160158,Android,Chrome,2,2,2,1,10,11,0E+00,0E+00
2021-03-01T00:48:37Z,24893358,Android,Chrome,4,4,4,4,4,8,0E+00,0E+00
2021-03-01T05:33:08Z,25006432,Android,Chrome,3,3,3,2,4,6,0E+00,0E+00
2021-03-01T05:07:40Z,24997184,Android,Chrome,4,4,4,4,2,6,0E+00,0E+00
2021-03-01T06:12:36Z,25021377,Android,Chrome,5,5,5,1,5,6,0E+00,0E+00
2021-03-01T16:09:14Z,25323922,Android,Chrome,3,3,3,2,3,5,0E+00,0E+00
2021-03-01T15:35:13Z,25303628,Android,Chrome,2,2,2,2,3,5,0E+00,0E+00
2021-03-01T06:48:23Z,25036224,Android,Chrome,5,5,5,5,0,5,0E+00,0E+00
2021-03-01T05:59:06Z,25015998,Android,Chrome,3,3,3,2,3,5,0E+00,0E+00</code></pre>

**GET STATISTICS BY DATE UNSUBSCRIBED (RANGE FORMAT)**

<pre><code>Sample Request: GET /v1/reports/push/users?dimensions=app_name&measures=wokenup,impressions,total_clicks,income&date_unsubscribed=2021-02-20|2021-02-28&sort=-wokenup&app_type=android

Authorization: Bearer [bearer_token]

Accept: text/csv</code></pre>

**GET STATISTICS BY LAST TOUCHED IN SPECIFIC HOUR (HOUR FORMAT)**

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
