### **Keyword Performance Metrics**
<a name="keyword_performance_metrics"></a>

### Resource Overview&nbsp;&nbsp;

|Method|URI Format|
|---|---|
|GET|/client_reports/keyword/[gmaid]?[query_params]|

Use GET to retrieve information for the Keyword report.  Data can be returned for a specific date range determined by start_date and end_date. The requirements for these parameters are described below.

The data returned will include totals for number of keywords, impressions, clicks, and click-through-rate (CTR), as well as a breakdown for each keyword.  Data will be returned in pages, controlled by the parameters page and page_size.  The first page is page 1.  Default values of 1 and 15 will be used if not specified.  Data is sorted in alphabetical order by keyword.

**Note: This API will not provide an Average page position from 1/1/2020 onward in the response.**

### Parameters&nbsp;&nbsp;

When using the GET method, the results can be filtered using these parameters:

|Parameter|Required|Description|
|---|---|---|
|start_date|Yes|Restricts the results to those occurring on or after this date|
|end_date|Yes|Restricts the results to those occurring on or before this date|
|global_master_campaign_id[]|Restrict results to one or more specific campaigns. This should be a comma separated string. Ex: global_master_campaign_id[]=TEST_1,TEST_2 <br>**Default value: all**|
|campaign_status[]|No|Restrict results to all campaigns with given status values.  Allowed values are running, stopped and ended. This should be a comma separated string. Ex: campaign_status[]=running,stopped <br>**Default value: all**|
|page_size|No|Restrict number of keywords in result <br>**Default value: 15**|
|page|No|Specifies which page of results to return <br>**Default value: 1**|
|sort_by|No|Specifies what column to sort by.  Valid columns are: keyword, clicks, impressions, and ctr <br>**Default value: keyword**|
|sort_dir|No|Specifies the sort direction.  Can be either asc or desc <br>**Default value: asc**|
|types[]|No|Specifies the campaign type of keyword.  Can be search, display or xmedia. Ex: types[]=display,search,xmedia <br>**Default value: search**|
|<internal> markup_type|Only supported value is 'percentage' </internal>|
|<internal> markup_value|"cost" fields (spend & budget) will be marked up by this pecentage </internal>|

### Response Data Details&nbsp;&nbsp;

> Retrieve data for a specific range of dates

```
curl -H "Authorization: Bearer OAUTH_ACCESS_TOKEN" \
https://api.localiqservices.com/client_reports/keyword/TEST_1?start_date=2016-12-01&end_date=2016-12-31&page=1&page_size=15
```

> Retrieve data for a specific campaign starting on a certain date

```
curl -g -H "Authorization: Bearer OAUTH_ACCESS_TOKEN" \
https://api.localiqservices.com/client_reports/keyword/TEST_1?global_master_campaign_id[]=TEST_1&start_date=2016-10-01&end_date=2016-12-31&page=1&page_size=15
```

> Retrieve data for campaigns that are stopped and running

```
curl -g -H "Authorization: Bearer OAUTH_ACCESS_TOKEN" \
https://api.localiqservices.com/client_reports/keyword/TEST_1?&campaign_status[]=running,stopped&start_date=2016-10-01&end_date=2016-12-31&page=1&page_size=15
```

> Retrieve data for both search and display campaigns

```
curl -g -H "Authorization: Bearer OAUTH_ACCESS_TOKEN" \
https://api.localiqservices.com/client_reports/keyword/TEST_1?types[]=display,search&start_date=2016-10-01&end_date=2016-12-31&page=1&page_size=15
```

> Example Response

```json
{
    "report_type": "keyword",
    "report_date": "2020-10-15",
    "earliest_date_available": "2020-01-01",
    "start_date": "2020-10-10",
    "end_date": "2020-10-10",
    "time_zone": "America/Los_Angeles",
    "report_data": {
        "totals": {
            "clicks": 17,
            "impressions": 1065,
            "ctr": 1.6,
            "keywords": 2
        },
        "keywords": [
            {
                "keyword": "Keyword (Demo) 1 Location (Demo) 1",
                "type": "search",
                "clicks": 6,
                "impressions": 383,
                "ctr": 1.57
            },
            {
                "keyword": "Keyword (Demo) 2 Location (Demo) 2",
                "type": "search",
                "clicks": 11,
                "impressions": 682,
                "ctr": 1.61
            }
        ]
    },
    "global_master_advertiser_id": "TEST_1",
    "location": "https://api.qa.localiqservices.com/client_reports/keyword/TEST_1?end_date=2020-10-10&start_date=2020-10-10",
    "page": 1,
    "page_size": 25
}
```

|Field Name|Datatype|Description|
|---|---|---|
|report_type|String|Name of the API|
|report_date|String|Date report was run|
|earliest_date_available|String|Earliest Data is Available|
|start_date|String|Start date of report|
|end_date|String|End date of report|
|time_zone|String|Time Zone|
|report_data|Object|Report details object containing Totals object and Campaigns array. [Report Data Object](#keywordreportdata)|
|global_master_advertiser_id|String|Identifier for advertiser|
|location|String|Location of this report|
|page|Int|Page Number|
|page_size|Int|Number of keywords on page|

<a name="keywordreportdata"></a>
**Report Data Object**

|Field Name|Datatype|Description|
|---|---|---|
|keywords|Keyword[]|[Array of Keyword](#keyword)|
|totals|Object|[Total Object](#totalkeyword)|

<a name="keyword"></a>
**Keyword Object**

|Field Name|Datatype|Description|
|---|---|---|
|keyword|Integer|Keyword Name|
|type|Integer|Keyword Type (search/display)|
|clicks|Float|Clicks for Keyword|
|impressions|Integer|Impressions for Keyword|
|ctr|Float|Click through Rate for Keyword|

<a name="totalkeyword"></a>
**Totals Object**

|Field Name|Datatype|Description|
|---|---|---|
|keywords|Integer|Number of total keywords regardless of page|
|clicks|Float|Overall Clicks|
|impressions|Integer|Overall Impressions|
|ctr|Float|Overall Click through Rate|
