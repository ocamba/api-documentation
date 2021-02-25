# Adex click report
host: api.ocamba.com

Use the /v1/reports/adex/click resource to get a custom report. A successful request returns the HTTP 200 OK status code and a JSON or CSV formatted response body. Response body format can be controlled by the HTTP Accept header. By default, this resource returns a CSV formatted response body.


# Dimensions
Dimensions are attributes of your data. 

Value is a string that can take multiple values separated by a comma. 

Maximum length: 100.

This parameter is optional. Default dimensions are click_date, bid_date, id, user_id, zone_id, campaign_id, ssp_account_id, dsp_account_id, creative_id, browser_name, os_name, subid, country_code, exchange_id, partner_id, ipv4, ipv6, landing_url, visitor_ua.

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| click_date | string |2020-12-03 02:05:12|The date of click.|
| bid_date | string |2020-12-03 02:04:00|The date of bid request.|
| diff | string |125|Difference between click_date and bid_date in seconds.|
| subid |string|source_example|String used to record and track unique user attributes, traffic sources, banners, and/or link placement.|
| zone_id |int|1009638|The ID of the zone.|
| zone_name |string|Push zone|The name of the zone.|
| exchange_id |int|936|The ID of the exchange.|
| exchange_name |string|ExampleExch POP|The name of the exchange.|
| partner_id |int|56|The ID of the partner.|
| partner_name |string|Example partner - Push CPC|The name of the partner.|
| request_id |int|68|The ID of the request.|
| placement_id |int|32|The ID of the placement.|
| os_id |int|12|The ID of the operating system.|
| os_name |string|Android|The name of the operating system.|
| browser_id |int|10|The ID of the browser.|
| browser_name |string|Chrome|The name of the browser.|
| campaign_id |int|1044852|The ID of the campaign.|
| campaign_name |string|Testing campaign|The name of the campaign.|
| creative_id |int|1000223|The ID of the creative.|
| creative_name |string|Testing creative|The name of the creative.|
| country_code |int|US|The code of the geographical country.|
| country_name |string|United States|The name of the geographical country.|
| id |int|xueh36baldj2|The ID of the session.|
| dsp_account_id |int|1000001|The ID of the demmand side platform account.|
| ssp_account_id |int|1000002|The ID of the supply side platform account.|
| ssp_account_name |string|Testing ssp account|The name of the supply side platform account.|
| dsp_account_name |string|Testing dsp account|The name of the demmand side platform account.|
| visitor_ua |string|Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.4 (KHTML, like Gecko) Chrome/22.0.1229.94 Safari/537.4|The visitor's user agent.|
| landing_url |string|www<span></span>.example.com|The landing_url of the click.|
| task_id |int|25845698|The ID of the task, only if the click was webpush.|
| date_delivery |int|2020-12-25 05:02:00|The date delivery, only if click was webpush.|
| ipv4 |string|37.8.65.98|The ipv4 of the user.|
| ipv6 |string|2001:0db8:85a3:0000:0000:8a2e:0370:7334|The ipv6 of the user.|
| connection_type |string|cable/dsl|The type of the connection.|
| conn_type_id |int|4|The ID of the connection type. (1 - 'dialup', 2 - 'cable/dsl', 3 - 'corporate', 4 - 'cellular')|
| asn |int|15169|The Autonomous System Number.|
| isp |string|Google|Internet Service Provider.|
| user_data_kv |string|ud_tpclk=example|Custom key-value map provided by requestor.|
| city_name |string|Sydney|The name of the city.|
| city_id |int|6354908|The GeoName ID of the city.| 

# Measures
This parameter represents the values that you're measuring. For example, you can measure app performance by looking at your earnings or number of clicks.

Value is a string that can take multiple values separated by a comma.

Maximum length: 100.

This parameter is optional. Default measures are income, expense.

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| income |float|16.52|The income of the click.|
| expense |float|16.52|The expense of the click.|
| revenue |float|16.52|The difference between income and expense.|


# Other parameters

These parameters are not required but can help with filtering, visualizing and making pivoting easier. 

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| sort |string|+delivered|Sort by field. Value should be one of the selected dimensions or measures.  "+" represents ascending order, "-" descending.| 
| page |string|2,10|The report can return data paginated by n items. In order to paginate through data, you can specify the “page” query parameter.|

## Report performance (IMPORTANT)

- **A wide date range will increase response time.**
- **The maximum date range is 7 days.**
- **The number of requested measures should not have a significant impact on report performance.**
