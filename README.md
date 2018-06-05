# iap-datadive-scoping
Repo for scoping and DataDive prep of IAP (International Accountability Project) DataDive Project. 

For more information see [Project Brief](https://docs.google.com/document/d/1r0n5Vh09N4QrXRs9QPfUaI6Bw-lWd3snTgomHhojA0E/edit)

## Data 
1. Feedly Data: Prior to DD we need to extract a large sample of feedly articles, see the 'Notebooks/Feedly_Extaction_Demo.ipynb' for starter code for this. File also includes the API token.  
    * The Feedly API allows for easy programmatic extraction of articles. They appear to limit individual “pulls” to 1000 items, but it also appears there are methods for retrieving older information. The actual IAP feed is relatively new and only contains around 500 articles, so the 1000 limit may be irrelevant. DataKind will generate a large sample of historical Feedly records.
2. EWS Data (Project Descriptions and MetaData):  This data should include all information related to project description.
    * This is the master project list that we can match articles to. 
    * ALSO: this dataset has project descriptions, etc that have been labeled with IAP Tags, this data could be used to help in assignment of tags to news articles. 
3. IAP Tag List
    * DataKind will work with IAP to build a list of “Tags” which may be useful for automatically stratifying news articles into specific groups.  In addition to the tags - we would require some logic for tags if they are communicating “higher level”  classification (oil, gas, coal → Energy extraction)
4. Article -> Article with Tags
    * DataKind and IAP will coordinate the development of small “test” datasets that volunteers can use to measure performance of tools. Ideally we would have around 100 articles labled with IAP Tags. 
5. Article -> Relevant Project 
    * DataKind and IAP will coordinate the development of small “test” datasets that volunteers can use to measure performance of tools. Ideally we would have around 100 articles manually matched to projects.


## Proposed Methodology/ies
To achieve the goal of automatically linking Feedly articles,or at least suggesting likely related articles, and assigning useful tags to relevant articles the following methodology is proposed.  

**Data Prep**

* Data Scientists will process the historic record of feedly articles (PRIOR TO DataDive)
* Determine if the article title and summary data contains enough information for project goals.If summary and title information do not provide enough information they may build simple scrapers to extract the content of the article. (PRIOR to DataDive)
* They will then featurize these data sources to allow for the calculation of similarity metrics with EWS project profiles, and for tagging. (Perhaps Some Prior to DataDive)
* Identify articles that are likely duplicates 
    * <<TODO - what is the logic for keeping one article over another ? Same url, same title ? or very similar content? (PRIOR to DataDive)
    * <<TODO - Should we also test the similarity between articles to identify that they are duplicates 
* Data Scientists will process the EWS project information
* Featurize this information to allow for similarity calculation with the Feedly data. 
* Tag with language - currently project information is in English so parsing articles in other languages in unnecessary - but tagging with language, sector and country would still be useful. (If possible - low priority)

**Tag Feedly Articles**
* Write code to automatically assign IAP determined tags to articles, current priority tags are: Country, Bank, Sector. 
* Some tags may simply be extracted based on the presence in the text, but other tags may be related to a more complex system of items, such as {oil, coal, mining}  may be related to a tag of “Energy Extraction”
* Transfer Learning  could potentially be applied to this problem but using the database of projects with tags and summaries to build a model that assigns tags to the news articles
* Determine how many potential matches to provide per de-duplicated article (perhaps just 2 projects) 


**Match to Projects**
* Filter projects (those that we search for being a match) based on some logical criteria, Perhaps related to tags (country, sector, city, etc) 
    - * Date/Status of project: Using data included in the EWS data, and the featurized Feedly data - Filter potential projects to those that are still active, would it be likely that a news article is being written about this project at this time, etc. 
* Generate Similarity Score Between Articles and Relevant Projects
* Identify reasonable cutoff metrics for suggesting a potential match
* In the absence of extensive labeled data “best judgement” should be used to identify reasonable cutoffs for suggesting a match. This logic may be clarified after initial similarity metrics are calculated and the results are examined. The smaller labeled test sets can be used to compare performance of different methods. 
* Identify how many potential matches to provide for review. 

**Output**
* The articles may then be grouped into specific “buckets” for dissemination to relevant IAP staff for final review. 
* Data should be machine readable unless IAP specifically requests text based output (automated report)

**Stretch Goals**
* Method for determining which articles have not been reviewed yet
Assuming this is run each day - we need to be able to constrain to only new articles, maybe this is based on the timestamp of the last run ? or some other constraint. 
    * How to record that information ?
        * DB
        * File
        * Rule (Example: always collects last 24 hours from 8am EST )
