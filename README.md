# Nosql-Challenge
The UK Food Standards Agency evaluates various establishments across the United Kingdom and gives them a food hygiene 
rating. We have been contracted by the editors of a food magazine, Eat Safe, Love, to evaluate some of the ratings data
in order to help their journalists and food critics decide where to focus future articles.

## Part 1: Database and Jupyter Notebook Set Up
Imported the data provided in the establishments.json file from my Terminal. Named the database uk_food and the 
collection establishments. Noted the text used to import your data from your Terminal to a markdown cell in your 
notebook.

Within the notebook, imported the libraries: PyMongo and Pretty Print (pprint).

Created an instance of the Mongo Client.

Confirmed that the database was created and then loaded the data properly:

Listed the databases you have in MongoDB. Confirm that uk_food is listed.
Listed the collection(s) in the database to ensure that establishments is there.
Found and displayed one document in the establishments collection using ```find_one``` and displayed with ```pprint```.
Assigned the establishments collection to a variable to prepare the collection for use.
 

## Part 2: Update the Database
The magazine editors requested some modifications for the database before performing any queries or analysis for them. 
Made the following changes to the establishments collection:

An exciting new halal restaurant just opened in Greenwich but hasn't been rated yet. The magazine asked to include it in 
the analysis. Added the following information to the database:


```    
    {
    "BusinessName":"Penang Flavours",
    "BusinessType":"Restaurant/Cafe/Canteen",
    "BusinessTypeID":"",
    "AddressLine1":"Penang Flavours",
    "AddressLine2":"146A Plumstead Rd",
    "AddressLine3":"London",
    "AddressLine4":"",
    "PostCode":"SE18 7DY",
    "Phone":"",
    "LocalAuthorityCode":"511",
    "LocalAuthorityName":"Greenwich",
    "LocalAuthorityWebSite":"http://www.royalgreenwich.gov.uk",
    "LocalAuthorityEmailAddress":"health@royalgreenwich.gov.uk",
    "scores":{
        "Hygiene":"",
        "Structural":"",
        "ConfidenceInManagement":""
    },
    "SchemeType":"FHRS",
    "geocode":{
        "longitude":"0.08384000",
        "latitude":"51.49014200"
    },
    "RightToReply":"",
    "Distance":4623.9723280747176,
    "NewRatingPending":True
}
```
Found the ```BusinessTypeID``` for "Restaurant/Cafe/Canteen" and returned only the ```BusinessTypeID``` and 
```BusinessType``` fields.

Updated the new restaurant with the ```BusinessTypeID``` found.

The magazine was not interested in any establishments in Dover, so checked how many documents contain the Dover Local 
Authority. Then, removed any establishments within the Dover Local Authority from the database, and checked the number 
of documents to ensure they were deleted.

Some of number values are stored as strings, when they should be stored as numbers.

Used ```update_many``` to convert latitude and longitude to decimal numbers.
Used ```update_many`` to convert ```RatingValue``` to integer numbers.

## Part 3: Exploratory Analysis
Eat Safe, Love has specific questions they want to be answered, which will help them find the locations they wish to 
visit and avoid.

```RatingValue``` refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, 
the better the rating.

The scores for Hygiene, Structural, and ConfidenceInManagement work in reverse. This means, the higher the value, the 
worse the establishment is in these areas.

Used the following questions to explore the database and found the answers to provide them to the magazine 
editors.

* Used count_documents to display the number of documents contained in the result.

* Displayed the first document in the results using pprint.

* Converted the result to a Pandas DataFrame, print the number of rows in the DataFrame, and display the first 10 rows.

* Which establishments have a hygiene score equal to 20?

* Which establishments in London have a RatingValue greater than or equal to 4?

* What are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new 
restaurant added - "Penang Flavours"?

* How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to 
lowest, and print out the top ten local authority areas.
