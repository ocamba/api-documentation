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
| event_date |string|2021-02-23|The date when the event have happened.|
| event_time |string|2021-02-23 14:00:00|The datetime when the event have happened.|
| postback_date |string|2021-02-23|The date when the pixel was fired.|
| postback_time |string|2021-02-23 14:00:00|The datetime when the pixel was fired.|
| url |string|http://<span></span>e-1234.example.net/r?e=eyJ0cyI6MTM2Mjc3MT|The pixel URL.|
| domain |string|e-1234.example.net|The domain of the pixel URL.|
| query |string|e=eyJ0cyI6MTM2Mjc3MT|The query of the pixel URL.|
| http_code |int|200|The HTTP code of the pixel response.|
| error_code |int|404|The error code of the pixel response.|
| event_type |string|push_sub|The event type, it can be adex_click, adex_imp, adex_conv, push_sub, push_unsub, push_wkup.|

# Measures
This parameter represents the values that you're measuring. For example, you can measure app performance by looking at your earnings or number of clicks.

Value is a string that can take multiple values separated by a comma.
This parameter is optional. Default dimensions are retries, incoming, outgoing.

Maximum length: 100.

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| pixel_count |int|2|The total number of fired pixels.|
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
| sort |string|+pixel_count|Sort by field. Value should be one of the selected dimensions or measures. "+" represents ascending order, "-" descending.| 
| page |string|2,10|The report can return data paginated by n items. In order to paginate through data, you can specify the “page” query parameter. The default setup is to return the first 100 results.|
| event_date |string|2020-12-08|Interval of time.<br>Single Format: Y-m-d<br>Range format: Y-m-d &#124; Y-m-d<br>Hour range format: Y-m-d hh:00:00 &#124; Y-m-d hh:00:00<br>Hour format: Y-m-d hh:00:00<br><br>If “single format” is used, the report displays stats for events which happened on this specific day.<br>If “range format” is used, the report displays stats for events which happened in this specific range.<br>If “hour format” is used, the report displays stats for events which happened in this specific hour.<br><br>For easier search, Reports API gives you the possibility of using one of the following labels:<br><ul><li>today</li><li>yesterday</li><li>last-7-days</li><li>last-30-days</li><li>last-24-hours</li><li>this-month</li><li>last-month</li></ul>|
| postback_date |string|2021-02-20 11:00:00|Interval of time.<br>Single Format: Y-m-d<br>Range format: Y-m-d &#124; Y-m-d<br>Hour range format: Y-m-d hh:00:00 &#124; Y-m-d hh:00:00<br>Hour format: Y-m-d hh:00:00<br><br>If “single format” is used, the report displays stats for pixels fired on this specific day.<br>If “range format” is used, the report displays stats for pixels fired in this specific range.<br>If “hour format” is used, the report displays stats for pixels fired in this specific hour.<br><br>For easier search, Reports API gives you the possibility of using one of the following labels:<br><ul><li>today</li><li>yesterday</li><li>last-7-days</li><li>last-30-days</li><li>last-24-hours</li><li>this-month</li><li>last-month</li></ul>|

# Examples
**GET RAW STATISTICS (LAST 100 FIRED PIXELS)**

<pre><code>Sample Request: GET /v1/reports/events?event_date=today&postback_date=today&sort=-event_time,-postback_time&page=1,100

Authorization: Bearer [bearer_token]

Accept: text/csv

Sample Response:

HTTP/1.1 200 OK

Content-Type: text/csv</code></pre>

**GET STATISTICS BY DATE RANGE (RANGE FORMAT)**

<pre><code>Sample Request: GET /v1/reports/events?sort=event_type,http_code&dimensions=event_type,http_code&measures=pixel_count&postback_date=2021-02-20|2021-02-21

Authorization: Bearer [bearer_token]

Sample Response:

HTTP/1.1 200 OK

event_type,http_code,pixel_count
push_sub,200,387535
push_unsub,200,9891
push_sub,404,911
push_sub,500,1
push_sub,520,7
push_unsub,520,1</code></pre>

**GET STATISTICS BY HOUR (HOUR FORMAT)**

<pre><code>Sample Request: GET /v1/reports/events?postback_date=2021-02-23 11:00:00&measures=pixel_count&dimensions=http_code,error_code&sort=http_code,error_code&event_type=push_sub&out=json

Authorization: Bearer [bearer_token]

Sample Response:

HTTP/1.1 200 OK

[
    {
        "http_code": "200",
        "error_code": "0",
        "pixel_count": 8575
    },
    {
        "http_code": "404",
        "error_code": "0",
        "pixel_count": 21
    },
    {
        "http_code": "500",
        "error_code": "0",
        "pixel_count": 1
    }
]</code></pre>

## Report performance (IMPORTANT)

- **If you want to get the data about fired pixels you should exclude dimensions and measures parameters.**
- **If both event_date and postback_date parameters are excluded, default setup displays "today" stats.**
- **A wide date range will increase response time.**
- **It's recommended not to use a date range wider than 7 days.**
- **The number of requested dimensions in the report will have an increasing effect on response time and the amount of data that will be generated by API.**
- **It's recommended to use a lower number of dimensions in reports.**
- **The number of requested measures should not have a significant impact on report performance.**