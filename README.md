# iap-datadive-scoping
Repo for IAP (International Accountability Project) DataDive Project. 

For more information see [Project Page](https://docs.google.com/document/d/1CpjzlksRqPjthfxRK5zENBCcNMRXS9hnTb5S_-WHSr0/edit?ts=5b294a34#heading=h.2gyhe3cbh4ek)

## Data 
**Also See [Data Dictionary](https://github.com/datakind/iap-datadive-scoping/blob/master/Data_Dictionary.md) **

1. **News Article Data --> `Data/Feedly_Processed_DF_cleaned...`**
    * The news article data has been extracted from Feedly ( a news aggregator application) used by IAP to collect articles realted to specific search terms they have created. This data was extracted from the Feedly API and then enriched with information on article text and article key words. See the Data Dictionary for more information on available fields and their meaning. This is the "raw" data that we want to enrich with:
        *   Tags (Bank, County, Sector)
        *   Match to Projects<br>
    **NOTE**: There are 3 versions of this data set, all with identical information<br>
        1.  a pickled Pandas DataFrame (py3.5) [`Feedly_Processed_DF_cleaned.pkl`]<br>
        2.  a pickled Pandas DataFrame (py2.7) [`Feedly_Processed_DF_cleaned_py27.pkl`] and a <br>
        3.  CSV [`Feedly_Processed_DF_cleaned.csv`]
2. **IAP Projects Data (EWS)  --> `Data/EWS_Published Project_Listing_DD.csv`**
    * The IAP Projects data was extracted from IAP's Early Warning System (EWS) database. This is the master project data that includes information on project description, release dates, country, sector, etc. One of goals is to match news articles to projects. This data also has tags for Bank, Sector and country - so could be used for transfer learning to build model predicting those tags. 
3. **Labeled Data** 
    * IAP has manually labeled a subset of News Articles. These labeled sets are segmented based on label. There are 4 files: one for each tag, and one for projects matched to news articles. 
        - Labeled Banks      --> `Data\Labeled_Data\banks.csv`
        - Labeled Sectors    --> `Data\Labeled_Data\sectors.csv`
        - Labeled Countries  --> `Data\Labeled_Data\countries.csv`
        - Labeled Projects   --> `Data\Labeled_Data\projects.csv`
4. **IAP Tag List** <br>
    **Sectors**
    ```
    agriculture and forestry 
    finance                          
    industry and trade          
    education and health                                
    *law and government          (not found in labeled data)
    *technical cooperation       (not found in labeled data)
    water and sanitation        
    communications               
    transport                   
    construction                 
    infrastructure
    hydropower              
    *climate and environment     (not found in labeled data)                   
    energy
    *mining                      (not found in labeled data)
    humanitarian response  
    MISC 
    ```

    **Banks**

    ```
    adb  : Asian Development Bank
    afdb : African Development Bank
    aiib : Asian Infrastructure Investment Bank
    ebrd : European Bank for Reconstruction and Development    
    eib  : European Investment Bank  
    *gcf : Green Climate Fund                      (not found in labeled data) 
    idb  : Inter-American Development Bank
    *iic : Inter-American Investment Corporation   (not found in labeled data)
    *ifc : International Finance Corporation       (not found in labeled data)
    *miga: Multilateral Investment Guarantee Agency(not found in labeled data)
    *fmo : Netherlands Development Finance Company (not found in labeled data)
    *ndb : New Development Bank                    (not found in labeled data)
    wb   : World Bank   
    ```

    
    **Countries**<br>
    ~80 Present in Labeled Data - more possible values in EWS projects data:

    ```
   ['afghanistan', 'africa', 'albania', 'albania, greece, italy',
       'angola', 'argentina', 'armenia', 'asia-pacific', 'azerbaijan',
       'bangladesh', 'bangladesh, india', 'bosnia',
       'botswana, ghana, kenya, zambia, lesotho, senegal,
        côte d’ivoire, nigeria, uganda, malawi, gabon and togo',
       'bulgaria', 'burkina faso', 'cambodia',
       'cambodia, mongolia, tajikistan', 'china', 'china, pakistan',
       'ecuador', 'egypt', 'ethiopia, kenya, nigeria, tanzania, uganda',
       'fiji', 'finland', 'gambia', 'georgia', 'georgia, ukraine',
       'ghana',
       'ghana, ethiopia, malawi, nigeria, mozambique and burkina faso.',
       'global', 'greece', 'greek', 'india', 'indina', 'indonesia',
       'iraq', 'jamaica', 'japan', 'jordan', 'kazakhstan', 'kenya',
       'kiribati', 'kyrgyzstan', 'lebanon', 'liberia', 'malawi',
       'maldives', 'micronesia', 'mongolia', 'montenegro', 'morocco',
       'morocco, tunisia', 'myanmar', 'nauru', 'nepal', 'nigeria',
       'pacific region', 'pakistan', 'papua new guinea', 'philippines',
       'romania', 'rwanda', 'serbia', 'somalia', 'sri lanka', 'sudan',
       'swaziland', 'tajikistan', 'thailand', 'timor-leste', 'tunisia',
       'turkenistan', 'turkey', 'turkey, azerbaijan, georgia',
       'turkey, greece, croatia', 'ukraine', 'uzbekistan', 'vietnam',
       'zambia', 'zimbabwe']
    ```



## Proposed Methodology/ies
* See [Project Page](https://docs.google.com/document/d/1CpjzlksRqPjthfxRK5zENBCcNMRXS9hnTb5S_-WHSr0/edit?ts=5b294a34#bookmark=id.fvby1pgpdve6)

## Goals (and some thoughts but be sure to review link above for more detail)

**Tag Feedly Articles**

* Write code to automatically assign IAP determined tags to articles
* Some tags may simply be extracted based on the presence in the text, but other tags may be related to a more complex system of items.
* Transfer Learning could potentially be applied to this problem but using the database of projects with tags and summaries to build a model that assigns tags to the news articles
* Determine how many potential matches to provide per de-duplicated article (perhaps just 2 projects) 


**Match to Projects**

* Filter projects (those that we search for being a match) based on some logical criteria, Perhaps related to tags (country, sector, city, etc) 
    - * Date/Status of project: Using data included in the EWS data, and the featurized Feedly data - Filter potential projects to those that are still active, would it be likely that a news article is being written about this project at this time, etc. 
* Generate Algorithm to identify possible matches between Articles and Projects
* Identify reasonable cutoff metrics for suggesting a potential match
* Identify how many potential matches to provide for review. 

