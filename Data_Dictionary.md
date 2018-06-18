
## Feedly Data
This data was extracted from feedly, then processed to extact article text, keywords and language. 

This is the "raw" data that needs to be matched with **Tags** (Banks, Sectors, Countries) and/or matched to **Projects** in the IAP-EWS database. 

```
article_id          : unique identifier for article (LINKING FIELD)
title               : Title of article as provided by the feedly API
url                 : url of article 
feed_label          : Label of the Feedly Feed (created by IAP)
content             : article content - as provided by feedly API (sparsely populated)
published           : date article was published 
summary             : summary info on article provided by feedly API 
article_text        : text of article as scraped from Newspaper3K library
article_keywords    : keywords of article as calculated from Newspaper3K library
article_text_len    : length of article text
top_lang            : detected language (all english)
```


## IAP-EWS Project Data 
This data was extracted from IAP's Early Warning System database. They would like to be able match this info to feedly article data to have more timely information on proejct updates. 

```
EWS ID                 : ID used internally IAPs system (ignore)
ProjectNumber          : ID used to match projects in this data to labeled projects (LINKING FIELD)
Published              : Date projects was published to IAP system
Bank Risk Rating       : Bank Risk Rating for project
Project Status         : Project Status
EWS URL                : URL on EWS system
Detailed Analysis URL  : Detailed Analysis URL
Project Name           : Project Name 
City                   : City of project (often null)
Country Count          : Count of Countries involved in project
Country 1              : First Country 
Country 2              : Second Country (if more than one)
Country 3              : Third Country (if more than one)
Country 4              : etc. (above)
Country 5              : etc. (above)
Country 6              : etc. (above)
Country 7              : etc. (above)
Country 8              : etc. (above)
Country 9              : etc. (above)
Country 10             : etc. (above)
Country 11             : etc. (above)
Country 12             : etc. (above)
Borrower or Client     : Entity that 
Private Actor Count    : Count of Private Actors involved with project (often null)
Private Actor 1        : First Private Actor
Private Actor 2        : etc.
Private Actor 3        : etc.
Private Actor 4        : etc.
...
Bank Count             : Count of Banks Involved
Bank 1                 : First Bank
Bank 2                 : Second Bank 
Bank 3                 : etc.
Bank 4                 : etc.
Bank 5                 : etc.
Sector Count           : Count of Relevant Sectors
Sector 1               : First Sector
Sector 2               : Second Sector
Sector 3               : etc.
Sector 4               : etc.
Sector 5               : etc.
Sector 6               : etc.
Sector 7               : etc.
Last Edited            : Date project information was last edited 
Date Scraped           : Date project information was scraped
Date Disclosed         : Date the project was disclosed by bank
Board Date             : Date the board will vote/review.
Source URL             : Scrape url
Project Cost           : Project Cost
Investment Amount      : Amount expeted to be invested by bank
Project Description    : Text description of project (USEFUL !!)
Contact Information    : More text description of contacts for the bank
```

<br>
------------------------------

<br>
## Labeled Data 
We want to be able to measure the performance of our models/algorithms. Therefore IAP manualy labeled the following datasets. One for each tag, plus one for projects. 

**Note**: There probably isn't enough data to train a model but there should be enough to evaluate performance. 

### Labeled Projects
```
article_id       : unique identifier for article (LINKING FIELD)
published        : date article was published
title            : Title of article as provided by the feedly API
url              : url of article 
feed_label       : Label of the Feedly Feed (created by IAP)
ProjectNumber    : Project ID number in EWS System (LINKING FIELD) - CAN BE MULTIPLE PROJECTS 
EWS Project Name : Project Name in EWS System
EWS hyperlink    : Link to Project in EWS System
Matched          : !IMPORTANT! Indicates if project is matched to article, 1 = match exists, 0 article has no \
                    matching project. Not all articles will match a project.  
```


### Labeled Articles -> Banks
```
article_id     : unique identifier for article (LINKING FIELD)
published      : date article was published
title          : Title of article as provided by the feedly API
url            : url of article 
feed_label     : Label of the Feedly Feed (created by IAP)
Bank1          : Bank associated with article
Bank2          : Second bank associated with article
```

### Labeled Articles -> Countries
```
article_id     : unique identifier for article (LINKING FIELD)
published      : date article was published
title          : Title of article as provided by the feedly API
url            : url of article 
feed_label     : Label of the Feedly Feed (created by IAP)
Country1       : Country(possibly more) associated with article
```

### Labeled Articles -> Sectors
```
article_id     : unique identifier for article (LINKING FIELD)
published      : date article was published
title          : Title of article as provided by the feedly API
url            : url of article 
feed_label     : Label of the Feedly Feed (created by IAP)
Sectors        : Sector(s) associated with article
cl_Sector      : Sector(s) but lowercased and whitespace stripped
top_sector     : First sector if multiple, or just the one sector listed. 
```
