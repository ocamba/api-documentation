# Adex reports
host: api.ocamba.com

Use the /reports/adex/ resource to get a custom report. A successful request returns the HTTP 200 OK status code and a JSON or CSV formatted response body. Response body format can be controlled by HTTP Accept header. By default, this resource returns CSV formatted response body.


# Dimensions
Dimensions are attributes of your data. Value is a string that can take multiple values separated by a comma. Maximum length: 100.

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| stat_date | string |2020-12-03|The date of the event.|
| subid |string|example_source|String used to record and track unique user attributes, traffic sources, banners, and/or link placement.|
| zone_id |int|1009638|The ID of the zone.|
| zone_name |string|Push zone|The name of the zone.|
| exchange_id |int|936|The ID of the exchange.|
| exchange_name |string|ExampleExchange POP|The name of the exchange.|
| partner_id |int|56|The ID of the partner.|
| partner_name |string|Example partner - Push CPC|The name of the partner.|
| campaign_id |int|1044852|The ID of the campaign.|
| campaign_name |string|Testing campaign|The name of the campaign.|
| creative_id |int|1000125|The ID of the creative.|
| creative_name |string|Testing creative|The name of the creative.|
| creative_lang |string|en|The language of the creative.|
| ssp_account_id |int|1000001|The ID of the supply side platform account.|
| ssp_account_name |string|Testing ssp account|The name of the supply side platform account.|
| ssp_pm |string|cpc|The pricing model of the supply side platform account.|
| dsp_account_id |int|1000002|The ID of the demmand side platform account.|
| dsp_account_name |string|Testing dsp account|The name of the demmand side platform account.|
| dsp_pm |string|cpm|The pricing model of the demmand side platform account.|
| country_code |int|US|The code of the geographical country.|
| country_name |string|United States|The name of the geographical country.|
| os_id |int|12|The ID of the operating system.|
| os_name |string|Android|The name of the operating system.|
| os_version |int|15|The major version of the operating system.|
| browser_id |int|10|The ID of the browser.|
| browser_name |string|Chrome|The name of the browser.|
| browser_version |int|87|The major version of the browser.|
| device_id |int|5|The ID of the device.|
| device_name |string|sony|The name of the device manufacturer.|
| user_lang |string|en|The language of the user.|
| tag |int|6|The ID of request type. (1 - 'open rtb', 5 - 'native', 6 - 'webpush')|
| connection_type |string|cable/dsl|The type of the connection.|
| conn_type_id |int|4|The ID of the connection type. (1 - 'dialup', 2 - 'cable/dsl', 3 - 'corporate', 4 - 'cellular')|
| asn |int|15169|The Autonomous System Number.|
| isp |string|Google|Internet Service Provider.|
| city_name |string|Sydney|The name of the city.|
| city_id |int|6354908|The GeoName ID of the city.|
| keyword |string|here goes example|Characteristic set of words or a phrase which describes the bid request.|

# Measures
This parameter represents the values that you're measuring. For example, you can measure campaign performance by looking at your earnings or number of clicks.

Value is a string that can take multiple values separated by a comma.
Maximum length: 100.

| parameter | type | example | description
| ------ | ---- | ------ | ----- |
| impression |int|15268|The total number of impressions.|
| total_click |int|1277|The total number of clicks (including spam).|
| click |int|1562|The total number of valid clicks.|
| spam_click |int|94|The total number of spam clicks.|
| conversion |int|12|The total number of conversions.|
| served |int|2435|The total number ad was returned in bid response.|
| request |int|2897|The total number of requests.|
| fill |int|2123|The total number of responses with at least one ad.|
| income |float|16.52|The gain derived from any dimension you requested.|
| expected_income |float|3.76|The expected gain derived from any dimension you requested.|
| expense |float|4.58|The cost incurred in the performance of the selected dimension.|
| revenue |float|11.98|The total earnings, the difference between income and expense.|
| ctr |float|0.15|The rate of clicks to impressions.|
| ftr |float|0.98|The rate of fill to requests.|
| ecpm |float|0.009|The rate of revenue to impressions.|

# Examples
**Get statistics by date (hourly breakdown of data)**

<pre><code>Sample Request: GET /v1/reports/adex?dimensions=stat_date&measures=impression,total_click,revenue&stat_date=2020-09-15
Authorization: Bearer [bearer_token]
Accept: text/csv

Sample Response:
HTTP/1.1 200 OK
Content-Type: text/csv

stat_date,impression,total_click,revenue
2020-09-15T19:00:00Z,35829065,60336,3.0306969E+02
2020-09-15T02:00:00Z,33042651,49677,2.3573848E+02
2020-09-15T12:00:00Z,41284335,70679,3.4215977E+02
2020-09-15T23:00:00Z,34008893,51378,2.8523679E+02
2020-09-15T17:00:00Z,38528334,63970,3.470948E+02
2020-09-15T13:00:00Z,42255910,74796,3.7689989E+02
2020-09-15T22:00:00Z,33461640,47598,2.7376716E+02
2020-09-15T16:00:00Z,40467343,66620,3.5177572E+02
…</code></pre>

**Get statistics by date Range(daily breakdown of data)**

<pre><code>Sample Request: GET /v1/reports/adex?dimensions=stat_date&measures=impression,total_click,revenue&stat_date=2020-09-15|2020-09-22
Authorization: Bearer [bearer_token]
Accept: text/csv

Sample Response:
HTTP/1.1 200 OK
Content-Type: text/csv

stat_date,impression,total_click,revenue
2020-09-15T00:00:00Z,866283539,1407089,6.57066276E+03
2020-09-16T00:00:00Z,838687856,1357293,6.37379728E+03
2020-09-17T00:00:00Z,646282886,1334215,6.14197825E+03
2020-09-18T00:00:00Z,609185985,1370410,6.10990207E+03
2020-09-19T00:00:00Z,609724900,1436969,5.04228602E+03
2020-09-20T00:00:00Z,614386656,1509305,5.51837149E+03
2020-09-21T00:00:00Z,599919921,1396536,6.41887398E+03</code></pre>

**Get statistics by CAMPAIGN**

<pre><code>Sample Request: GET /v1/reports/adex?dimensions=campaign_id&measures=impression,total_click,revenue&stat_date=2020-09-15|2020-09-22
Authorization: Bearer [bearer_token]
Accept: text/csv</code></pre>

**Get statistics by subid (filtered by campaign_ID)**

<pre><code>Sample Request: GET /v1/reports/adex?dimensions=subid&measures=impression,total_click,revenue&stat_date=2020-09-20|2020-09-22&campaign_id=1000000
Authorization: Bearer [bearer_token]
Accept: text/csv</code></pre>

**Get statistics by OS (sorted by Impressions)**

<pre><code>Sample Request: GET /v1/reports/adex?dimensions=os_id&measures=impression,total_click,revenue&stat_date=2020-09-20|2020-09-22&sort=impression
Authorization: Bearer [bearer_token]
Accept: text/csv</code></pre>

**Get statistics by OS (sorted by Impressions AND LIMITED to 10 results)**

<pre><code>Sample Request: GET /v1/reports/adex?dimensions=os_id&measures=impression,total_click,revenue&stat_date=2020-09-20|2020-09-22&sort=impression&page=1,10
Authorization: Bearer [bearer_token]
Accept: text/csv</code></pre>
