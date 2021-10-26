# Push reports
host: api.ocamba.com

Use the /reports/push/ resource to get a custom report. A successful request returns the HTTP 200 OK status code and a JSON or CSV formatted response body. Response body format can be controlled by HTTP Accept header. By default, this resource returns CSV formatted response body.


# Dimensions
Dimensions are attributes of your data. Value is a string that can take multiple values separated by a comma. Maximum length: 100.

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| stat_date | string |2021-09-03|The date of the event.|
| delivery_date | string |2021-09-03|The date of the scheduler delivery created on Ocamba platform.|
| task_id |int|5623871|Push scheduler id created on Ocamba platform.|
| task_name |string|Scheduler test #1|Push scheduler name created on Ocamba platform.|
| app_id |int|126598752|Push app id created on Ocamba platform.|
| app_name |string|test.demo.com|Push app name created on Ocamba platform.|
| traffic_id |int|1010126|Push traffic id created on Ocamba platform.|
| country_code |string|US|The code of the geographical country supported by Ocamba.|
| country_name |string|United States|The name of the geographical country supported by Ocamba.|
| lang_code |string|it|The code of the language supported by Ocamba.|
| lang_name |string|Italian|The name of the language supported by Ocamba.|
| os_id |int|12|The operating system id supported by Ocamba.|
| os_name |string|Android|The operating system name supported by Ocamba.|
| browser_id |int|10|The browser id supported by Ocamba.|
| browser_name |string|Chrome|The browser name supported by Ocamba.|
| conn_type |string|cable/dsl|The type of the connection supported by Ocamba.|
| conn_type_id |int|4|The ID of the connection type. (1 - 'dialup', 2 - 'cable/dsl', 3 - 'corporate', 4 - 'cellular')|
| asn |int|15169|The Autonomous System Number supported by Ocamba.|
| isp |string|Google|Internet Service Provider supported by Ocamba.|
| city_name |string|Sydney|The name of the city supported by Ocamba.|
| city_id |int|6354908|The GeoName ID of the city supported by Ocamba.|
| app_type |string|web|The application type of user (web, android, ios).|

# Measures
This parameter represents the values that you're measuring. For example, you can measure application performance by looking at your number of clicks.

Value is a string that can take multiple values separated by a comma.
Maximum length: 100.

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| click |int|1562|The total number of clicks.|
| wokenup |int|2435|The total of times user was received message from cloud.|
| ctr |decimal|154|The rate of clicks to wokenups.|
| subscriptions |int|2128|The total number of user subscriptions.|
| unsubscriptions |int|154|The total number of user unsubscriptions.|
| user_growth |int|154|Growth scale of the user base that represents a ratio between subscribed and unsubscribed users. A ratio can be negative since there is a possibility that there are more unsubscribed users than subscribed in a particular time range.|

# Other parameters

These parameters are not required but can help with filtering, visualizing, and making pivoting easier.

| parameter | type | example | description |
| ------ | ---- | ------ | ----- |
| stat_date|string|2020-12-08|Interval of time.<br>Single Format: Y-m-d<br>Range format: You should use one of the [range operators](#operators) -> rf:Y-m-d,Y-m-d<br>Hour range format: rl:Y-m-d hh:00:00,Y-m-d hh:00:00<br><br>If “single format” is used, the report displays stats for this specific day.<br>If “range format” is used, the report displays stats in this specific range.<br>If “hour range format” is used, the report displays stats in this specific range by hours.<br><br>If you exclude this parameter, the default setup displays "today" stats.|
| resolution|string|hour|This parameter additionally defines the stat_date parameter. You should pass `day` or `hour`, which defines what type of breakdown you request, default setup displays daily breakdown. If day is passed, the report displays stats for specific range by days. If hour is passed, the report displays stats for specific range by hour. If you pass the stat_date in the hour format and request the daily resolution, the stat_date will have priority over the resolution.|

# Operators 
<a name="operators"></a>
| operator | description | behavior |
| --- | ----- | -------- |
| r|range|The value must be in a specified open range, where both endpoints are excluded.|
| rf|range full|The value must be in a specified closed range, where both endpoints are included.|
| rl|range left|The value must be in a specified half-open range, where only left or start point is included.|
| rr|range right|The value must be in a specified half-open range, where only right or end point is included.|

# Examples
**Get statistics by date (hourly breakdown of data)**

<pre><code>Sample Request: GET /v1/reports/push?dimensions=stat_date,app_id&measures=wokenup,subscriptions&stat_date=today
Authorization: Bearer [bearer_token]
Accept: text/csv

Sample Response:
HTTP/1.1 200 OK
Content-Type: text/csv

stat_date,app_id,wokenup,subscriptions
2021-09-09T03:00:00Z,430565321,23812,2
2021-09-09T02:00:00Z,297684803,207670,77
2021-09-09T03:00:00Z,3325452325,102832,0
2021-09-09T02:00:00Z,4333546932,102,0
2021-09-09T06:00:00Z,5868648829,221331,62
2021-09-09T07:00:00Z,459546475,114292,34
2021-09-09T04:00:00Z,963033338,10512,12
2021-09-09T06:00:00Z,5658555800,360085,108
2021-09-09T05:00:00Z,11654657043,33843,33
2021-09-09T05:00:00Z,975586638,331535,0
…</code></pre>

**Get statistics by date Range(daily breakdown of data)**

<pre><code>Sample Request: GET /v1/reports/push?dimensions=stat_date&measures=wokenup,click&stat_date=rf:2021-10-24,2021-10-25
Authorization: Bearer [bearer_token]
Accept: text/csv

Sample Response:
HTTP/1.1 200 OK
Content-Type: text/csv

stat_date,wokenup,click
2021-09-07T00:00:00Z,280735260,3524
2021-09-08T00:00:00Z,593671037,3481
2021-09-09T00:00:00Z,221796899,3987
</code></pre>