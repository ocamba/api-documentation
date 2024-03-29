# Exchange reports
host: api.ocamba.com

Use the /v1/reports/adex/exchange resource to get a custom report. A successful request returns the HTTP 200 OK status code and a JSON or CSV formatted response body. Response body format can be controlled by the HTTP Accept header. By default, this resource returns a CSV formatted response body.


# Dimensions
Dimensions are attributes of your data. 

Value is a string that can take multiple values separated by a comma. 

Maximum length: 100.

| parameter | type | example | description |
| ------ | ---- | ------ | ----- |
| stat_date|string|2021-01-20 11:00:00|Request time.|
| exchange_id|int|348|The ID of the exchange.|
| exchange_name|string|ExampleExchange POP|The name of the exchange.|
| partner_id|int|157|The ID of the exchange partner.|
| partner_name|string|Example partner - Push CPC|The name of the exchange partner.|
| subid|string|example_source|String used to record and track unique user attributes, traffic sources, banners, and/or link placement.|
| os_id|int|4|The ID of the operating system supported by the Ocamba platform.|
| os_name|string|Mac OS X|The name of the operating system supported by the Ocamba platform.|
| browser_id|int|12|The ID of the browser supported by the Ocamba platform.|
| browser_name|string|Chrome|The name of the browser supported by the Ocamba platform.|
| country_code|string|US|The two-letter country code of the particular country you need data for.|
| country_name|string|United States|Full name of the particular country you need data for.|
| device_id|int|4|The ID of the device supported by the Ocamba platform.|
| device_name|string|SAMSUNG|The name of the device supported by the Ocamba platform.|
| campaign_id |int|1044852|The ID of the campaign.|
| campaign_name |string|Testing campaign|The name of the campaign.|
| zone_id |int|1009638|The ID of the zone.|
| zone_name |string|Push zone|The name of the zone.|


# Measures
This parameter represents the values that you're measuring. For example, you can measure exchange performance by looking at your earnings or number of clicks.

Value is a string that can take multiple values separated by a comma.

Maximum length: 100.

| parameter | type | example | description |
| ------ | ---- | ------ | ----- |
| success|int|22674|The total number of requests which successfully returned an ad.|
| failed|int|135|The total number of requests which failed to return a valid ad.|
| impression|int|15268|The total number of impressions.|
| total_click|int|1656|The total number of clicks (including spam).|
| click|int|1562|The total number of valid clicks.|
| spam_click|int|94|The total number of spam clicks.|
| ctr|float|10.84|The rate of clicks to impressions.|
| conversion|int|12|The total number of conversions.|
| income|float|16.52|The gain derived from the exchange, exchange partner, etc.|
| expense|float|1.33|The cost incurred in the performance of the exchange.|
| revenue|float|15.19|The total earnings, the difference between income and expense.|

# Other parameters

These parameters are not required but can help with filtering, visualizing, and making pivoting easier.

| parameter | type | example | description |
| ------ | ---- | ------ | ----- |
| exchange_id|string|1002600|Exchange id created on the Ocamba platform. This parameter can be used to filter your data by the specific exchange.|
| partner_id|string|1002600|Exchange partner id created on the Ocamba platform. This parameter can be used to filter your data by the specific exchange partner.|
| subid|string|filter_source|This parameter can be used to filter your data by the specific subid/source.|
| os_id|int|4|This parameter can be used to filter your data by the specific operating system.|
| browser_id|int|12|This parameter can be used to filter your data by the specific browser.|
| country_code|string|FR|This parameter can be used to filter your data by the specific country.|
| device_id|int|4|This parameter can be used to filter your data by the specific device.|
| sort|string|+success|Sort by field. The value should be one of the selected dimensions or measures. "+" represents ascending order, "-" descending.| 
| page|string|2,10|The report can return data paginated by n items. In order to paginate through data, you can specify the “page” query parameter.|
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
**GET STATISTICS BY DATE (SINGLE FORMAT)**

<pre><code>Sample Request: GET /v1/reports/adex/exchange?dimensions=exchange_name&measures=impression,total_click,income&stat_date=2021-02-01

Authorization: Bearer [bearer_token]

Accept: text/csv

Sample Response:

HTTP/1.1 200 OK

Content-Type: text/csv</code></pre>

**GET STATISTICS BY DATE RANGE (RANGE FORMAT)**

<pre><code>Sample Request: GET /v1/reports/adex/exchange?dimensions=stat_date,partner_name&measures=success,failed&stat_date=rf:2021-01-10,2021-01-15
Authorization: Bearer [bearer_token]
Accept: text/csv</code></pre>

**GET STATISTICS BY HOUR (HOUR FORMAT)**

<pre><code>Sample Request: GET /v1/reports/adex/exchange?dimensions=stat_date,subid&measures=click,spam_click&sort=-click&stat_date=2021-02-02&resolution=hour
Authorization: Bearer [bearer_token]
Accept: text/csv</code></pre>

**GET LAST STATISTICS (WHERE FAILED REQ IS GREATER THAN 0)**

<pre><code>Sample Request: GET /v1/reports/adex/exchange?dimensions=stat_date,exchange_name&measures=failed&sort=-failed&failed=gt:0
Authorization: Bearer [bearer_token]
Accept: text/csv</code></pre>

**GET STATISTICS FILTERED BY SUBID**

<pre><code>Sample Request: GET /v1/reports/adex/exchange?dimensions=stat_date,partner_name,exchange_name&measures=impression,total_click,ctr,income&sort=-stat_date&stat_date=rf:2021-02-01,2021-02-10&subid=source_example
Authorization: Bearer [bearer_token]
Accept: text/csv</code></pre>

**GET TOP TEN EXCHANGE PARTNERS BY REVENUE IN LAST 30 DAYS**

<pre><code>Sample Request: GET /v1/reports/adex/exchange?dimensions=partner_name&measures=revenue&sort=-revenue&stat_date=last-month&page=1,10
Authorization: Bearer [bearer_token]
Accept: text/csv</code></pre>

## Report performance (IMPORTANT)

- **A wide date range will increase response time.**
- **The maximum date range is 30 days.**
- **The number of requested dimensions in the report will have an increasing effect on response time and the amount of data that will be generated by API.**
- **It's recommended to use a lower number of dimensions in reports.**
- **The number of requested measures should not have a significant impact on report performance.**
