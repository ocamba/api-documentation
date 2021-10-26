# Events postback reports
host: api.ocamba.com

Use the /v1/reports/events resource to get a custom report. A successful request returns the HTTP 200 OK status code and a JSON or CSV formatted response body. Response body format can be controlled by the HTTP Accept header. By default, this resource returns a CSV formatted response body.

# Dimensions
Dimensions are attributes of your data. 

Value is a string that can take multiple values separated by a comma. 
This parameter is optional. Default dimensions are event_time, postback_time, url, domain, query, http_code, error_code, event_type.

Maximum length: 100.

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| event_date |string|2021-02-23|The date when the event has happened.|
| event_time |string|2021-02-23 14:00:00|The datetime when the event has happened.|
| postback_date |string|2021-02-23|The date when the postback was fired.|
| postback_time |string|2021-02-23 14:00:00|The datetime when the postback was fired.|
| url |string|http://<span></span>e-1234.example.net/r?e=eyJ0cyI6MTM2Mjc3MT|The postback URL.|
| domain |string|e-1234.example.net|The domain of the postback URL.|
| query |string|e=eyJ0cyI6MTM2Mjc3MT|The query of the postback URL.|
| http_code |int|200|The HTTP code of the postback response.|
| error_code |int|404|The error code of the postback response.|
| event_type |string|push_sub|The event type, it can be adex_click, adex_imp, adex_conv, push_sub, push_unsub.|

# Measures
This parameter represents the values that you're measuring. 

Value is a string that can take multiple values separated by a comma.
This parameter is optional. Default dimensions are retries, incoming, outgoing.

Maximum length: 100.

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| postback_count |int|2|The total number of fired postbacks.|
| inc_bandwidth |int|12743036|The total number of incoming bandwidth.|
| out_bandwidth |int|19300365|The total number of outgoing bandwidth.|
| retries_count |int|53881|The total number of retried requests.|


# Other parameters

These parameters are not required. 

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| url |string|http://<span></span>e-1234.example.net/r?e=eyJ0cyI6MTM2Mjc3MT|This parameter can be used to filter your data by the specific URL.|
| domain |string|e-1234.example.net|This parameter can be used to filter your data by the specific domain.|
| query |string|e=eyJ0cyI6MTM2Mjc3MT|This parameter can be used to filter your data by the specific query.|
| http_code |int|200|This parameter can be used to filter your data by the specific HTTP code.|
| error_code |int|404|This parameter can be used to filter your data by the specific error code.|
| event_type |string|adex_click|This parameter can be used to filter your data by the specific event type.|
| sort |string|+postback_count|Sort by field. The value should be one of the selected dimensions or measures. "+" represents ascending order, "-" descending.| 
| page |string|2,10|The report can return data paginated by n items. In order to paginate through data, you can specify the “page” query parameter. The default setup is to return the first 100 results.|
| event_date |string|2020-12-08|Interval of time.<br>Single Format: Y-m-d<br>Range format: You should use one of the [range operators](#operators) -> rf:Y-m-d,Y-m-d<br>Hour range format: rl:Y-m-d hh:00:00,Y-m-d hh:00:00<br>Hour format: Y-m-d hh:00:00<br><br>If “single format” is used, the report displays stats for events that happened on this specific day.<br>If “range format” is used, the report displays stats for events that happened in this specific range.<br>If “hour format” is used, the report displays stats for events that happened in this specific hour.<br><br>For easier search, Reports API gives you the possibility of using one of the following labels:<br><ul><li>today</li><li>yesterday</li><li>last-7-days</li><li>last-30-days</li><li>last-24-hours</li><li>this-month</li><li>last-month</li></ul>|
| postback_date |string|2021-02-20 11:00:00|Interval of time.<br>Single Format: Y-m-d<br>Range format: You should use one of the [range operators](#operators) -> rf:Y-m-d,Y-m-d<br>Hour range format: rl:Y-m-d hh:00:00,Y-m-d hh:00:00<br>Hour format: Y-m-d hh:00:00<br><br>If “single format” is used, the report displays stats for postbacks fired on this specific day.<br>If “range format” is used, the report displays stats for postbacks fired in this specific range.<br>If “hour format” is used, the report displays stats for postbacks fired in this specific hour.<br><br>For easier search, Reports API gives you the possibility of using one of the following labels:<br><ul><li>today</li><li>yesterday</li><li>last-7-days</li><li>last-30-days</li><li>last-24-hours</li><li>this-month</li><li>last-month</li></ul>|

# Operators 
<a name="operators"></a>
| operator | description | behavior |
| --- | ----- | -------- |
| r|range|The value must be in a specified open range, where both endpoints are excluded.|
| rf|range full|The value must be in a specified closed range, where both endpoints are included.|
| rl|range left|The value must be in a specified half-open range, where only left or start point is included.|
| rr|range right|The value must be in a specified half-open range, where only right or end point is included.|

# Examples
**GET RAW STATISTICS (LAST 100 FIRED POSTBACKS)**

<pre><code>Sample Request: GET /v1/reports/events?event_date=today&postback_date=today&sort=-event_time,-postback_time&page=1,100

Authorization: Bearer [bearer_token]

Accept: text/csv

Sample Response:

HTTP/1.1 200 OK

Content-Type: text/csv</code></pre>

**GET STATISTICS BY DATE RANGE (RANGE FORMAT)**

<pre><code>Sample Request: GET /v1/reports/events?sort=event_type,http_code&dimensions=event_type,http_code&measures=postback_count&postback_date=rf:2021-02-20,2021-02-23

Authorization: Bearer [bearer_token]

Sample Response:

HTTP/1.1 200 OK

event_type,http_code,postback_count
push_sub,200,387535
push_unsub,200,9891
push_sub,404,911
push_sub,500,1
push_sub,520,7
push_unsub,520,1</code></pre>

**GET STATISTICS BY HOUR (HOUR FORMAT)**

<pre><code>Sample Request: GET /v1/reports/events?postback_date=rl:2021-10-23 11:00:00,2021-10-23 12:00:00&measures=postback_count&dimensions=http_code,error_code&sort=http_code,error_code&event_type=push_sub&out=json

Authorization: Bearer [bearer_token]

Sample Response:

HTTP/1.1 200 OK

[
    {
        "http_code": "200",
        "error_code": "0",
        "postback_count": 8575
    },
    {
        "http_code": "404",
        "error_code": "0",
        "postback_count": 21
    },
    {
        "http_code": "500",
        "error_code": "0",
        "postback_count": 1
    }
]</code></pre>

## Report performance (IMPORTANT)

- **If you want to get the data about fired postbacks you should exclude dimensions and measures parameters.**
- **If both event_date and postback_date parameters are excluded, the default setup displays "today" stats.**
- **A wide date range will increase response time.**
- **It's recommended not to use a date range wider than 7 days.**
- **The number of requested dimensions in the report will have an increasing effect on response time and the amount of data that will be generated by API.**
- **It's recommended to use a lower number of dimensions in reports.**
- **The number of requested measures should not have a significant impact on report performance.**
