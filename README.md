# DATA 512 Assignment A1
Emily Yamauchi


## Introduction

### Objective

The goal of this assignment is to construct, analyze, and publish a dataset of monthly traffic of English Wikipedia from Jaunary 1 2008 to August 31 2021. 
The data is combined from two different [Wikimedia REST API](https://www.mediawiki.org/wiki/REST_API) into a single dataset, which then goes through simple data processing, and finally is analyzed as a time series visualization.


### Data Source

Data is collected from two different Wikimedia REST API.  
- The Legacy Pagecounts API ([documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts), [endpoint](https://wikimedia.org/api/rest_v1/#!/Pagecounts_data_(legacy)/get_metrics_legacy_pagecounts_aggregate_project_access_site_granularity_start_end)) provides access to desktop and mobile traffic data from December 2007 through July 2016.
- The Pageviews API ([documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews), [endpoint](https://wikimedia.org/api/rest_v1/#!/Pageviews_data/get_metrics_pageviews_aggregate_project_access_agent_granularity_start_end)) provides access to desktop, mobile web, and mobile app traffic data from July 2015 through last month.  

The terms and conditions of the API can be viewed [here](https://www.mediawiki.org/wiki/Wikimedia_REST_API#Terms_and_conditions).

### Data Processing

The collected JSON file is processed through the following steps:  

- combined into single data structure
- data structure is pivoted to show access type as columns
- mobile access is aggregated as single type (web and app)
- views for both pagecount and pageview are aggregated as totals

The fields in the cleaned dataset is as follows:  

| Column      | Value |
| :----------- | :----------- |
| year      | YYYY       |
| month   | MM        |
|pagecount_all_views |num_views|
|pagecount_desktop_views| num_views|
|pagecount_mobile_views |num_views|
|pageview_all_views |num_views |
|pageview_desktop_views | num_views |
|pageview_mobile_views | num_views |

### Known Issues

The aggregation methodology changed in May 2015. The legacy pagecounts reported user traffic and automated traffics together.  
In the visualization, the dotted lines indicate old definition of pagecounts, while the solid lines indicate the new definition which eliminated all crawler traffic.  
More information regarding the old legacy pagecount definition can be viewed [here](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts)



### Folder Structure

```
 data-512-a1
    ├── LICENSE
    ├── README.md
    ├── data_raw
    │   ├── pagecounts_desktop-site_2007120100-2016080100.json
    │   ├── pagecounts_mobile-site_2007120100-2016080100.json
    │   ├── pageviews_desktop_2015070100-2016080100.json
    │   ├── pageviews_mobile-app_2015070100-2021100100.json
    │   └── pageviews_mobile-web_2015070100-2021100100.json
    ├── data_clean
    │   └── en-wikipedia_traffic_200712-202109.csv
    ├── visualization
    │   └── plot.png
    └── hcds-a1-data-curation.ipynb
```