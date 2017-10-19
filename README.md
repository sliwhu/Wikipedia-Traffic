# English Wikipedia Monthly Traffic Collection and Analysis  

### Project Goal  
This project aims to construct, analyze, and publish a dataset of monthly traffic on English Wikipedia from July 1 2008 through September 30 2017.  

### Project Overview  
This project is consisted of three steps:
* ##### data acquision
  Data was collected from two different API endpoints, the Pagecounts API and the Pageviews API. In May 2015, a new pageview definition took effect, which eliminates all crawler traffic. The Pageviews API allows us to access the data under new definition, while the Pagecounts API stores the legacy pageview data.
* ##### data processing 
  A series of processing steps were performed on the data files from step 1 to prepare them for analysis, including but not limited to read json file into python dataframe, extract year, month and count data, combine desktop and mobile views. Export data into "en-wikipedia_traffic_200801-201709.csv".
* ##### data analysis
  A graph visualization was produced and track three traffic metrics: mobile traffic, desktop traffic, and all traffic (mobile + desktop)  on both legacy pagecounts and pageviews from July 1 2008 through September 30 2017.

The details of each step is illustrated in the "Wikipedia_Monthly_Traffic.ipynb".     

### Project Structure
```
English Wikipedia Monthly Traffic Collection and Analysis/  
  |- Data/  
     |- pagecounts_desktop-site_200801-201607.json  
     |- pagecounts_mobile-site_200801-201607.json   
     |- pageviews_desktop_201507-201709.json  
     |- pageviews_mobile-web_201507-201709.json  
     |- pageviews_mobile-app_201507-201709.json  
     |- en-wikipedia_traffic_200801-201709.csv  
  |- LICENSE
  |- README.md
  |- Wikipedia_Monthly_Traffic.ipynb
  |- Finalplot.png   
```

### Source Data Licensing 
Data was gathered from the Wikimedia REST API,
Wikimedia Foundation, 2017. CC-BY-SA 3.0.
See the Wikimedia Terms of Use for more details:
https://wikimediafoundation.org/wiki/Terms_of_Use/en

### Source Data API documentation
Data was collected from two different API endpoints, the Pagecounts API and the Pageviews API.

The legacy Pagecounts API ([documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts), [endpoint](https://wikimedia.org/api/rest_v1/#!/Pagecounts_data_(legacy)/get_metrics_legacy_pagecounts_aggregate_project_access_site_granularity_start_end)) provides access to desktop and mobile traffic data from January 2008 through July 2016.
The Pageviews API ([documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews), [endpoint](https://wikimedia.org/api/rest_v1/#!/Pageviews_data/get_metrics_pageviews_aggregate_project_access_agent_granularity_start_end)) provides access to desktop, mobile web, and mobile app traffic data from July 2015 through September 2017.

### Data Output 
The analyzed results were stored in a single CSV file named "en-wikipedia_traffic_200801-201709.csv"


|        Column         |        Value        |
|-----------------------|---------------------|
|         year	        |         YYYY        |
|         month	        |          MM         |
|   pagecount_all_views	|       num_views     |
|pagecount_desktop_views|       num_views     |
|pagecount_mobile_views |       num_views     |
|   pageview_all_views	|       num_views     |
|pageview_desktop_views |       num_views     |
|pageview_mobile_views  |       num_views     |

**Year**: four-digit year (YYYY) range from 2008 to 2017.  
**Month**: two-digit month (MM) range from 2008-01 to 2017-09   
**Pagecount_all_views**: data collected from the legacy Pagecounts API, combine the monthly values for desktop-site and mobile-site to create a total mobile traffic count for each month.  
**Pagecount_desktop_views**: data collected from the Pageviews API, desktop traffic count for each month.  
**Pagecount_mobile_views**: data collected from the Pageviews API, mobile traffic count for each month.  
**Pageview_all_views**: data collected from the Pageviews API, combine the monthly values for desktop, mobile-app and mobile-web to create a total mobile traffic count for each month.  
**Pageview_desktop_views**: data collected from the Pageviews API, desktop traffic count for each month.  
**Pageview_mobile_views**: data collected from the Pageviews API, combine the monthly values for mobile-app and mobile-web to create a total mobile traffic count for each month.  


### Special Considerations in Data Analysis
* ##### Legacy pagecounts data is available from January 2008 through July 2016. Pageviews data is available from July 2015 through September 2017. Therefore, there is an overlap records from July 2015 to July 2016 with different traffic measurements. 
* ##### Both data from the Pageview API and Pagecount API is segmented to desktop and mobile traffic. The mobile traffic for the Pageviews was a combination of mobile-app and mobile-web traffic. A total pageview of combining desktop and mobile views was included in the final data output ("en-wikipedia_traffic_200801-201709.csv") as well as in the final graph.
* ##### Data from the Pageview API excludes spiders/crawlers, while data from the Pagecounts API does not.
* ##### For all months with 0 pageviews for a given access method (e.g. desktop-site, mobile-app), that value for that (column, month) was listed as 0 in the final data output ("en-wikipedia_traffic_200801-201709.csv"). So for example all values of pagecount_mobile_views for months before October 2014 are 0, because mobile traffic data is not available before that month.
* ##### The analysis result is presented in a graph with three metrics: mobile traffic, desktop traffic, and all traffic(mobile + desktop), as well as two sources (Pagecount API and Pageview API, represented by dashed and solid lines respectively.)

