---
title: "Geocoding in OpenRefine using an API"
teaching: 5
exercises: 0
questions:
- "What are other ways to create new data based on a column?"
- "How can we parse formatted data in OpenRefine?"
- "Are there ways we can use an API in OpenRefine to find inconsistencies?"
objectives:
- "Create a column using existing data and a call to an API."
- "Parse data from JSON into two columns; latitude and longitude."
keypoints:
- "OpenRefine and the GeoNames API can be combined to do basic geocoding."
---
# Lesson

## Combine columns

Combining columns is not as intuitive as you might expect it to be. We  are going to combine our cleaned up `City` and `State` data to create one column that we can use as the basis for our search using the GeoNames API. To concatenate strings in two columns, we can use the `+`. This also works for other text that we would like to add, which has to be put in `""`. 

>## Exercise
>
> 1. Click on the down arrow in the `City` column and choose `Edit column` > `Add column based on this column`.
> 2. Give the new column the name `City_State`.
> 3. We want the text from the `City` column (value), the text from the `State` column, and a `, ` in between. Our expression is:
>
> >## Solution
> > ```value  + ", " + cells["State"].value```
> {: .solution}
>
> 4. Leave the default `set to blank` if the process doesn't work. The preview should show `City, ST`. If it doesn't, check your expression.
> 5. Click `OK` 
>
{: .challenge}

## Use existing data to get data from a website

For this demo I am going to use a spreadsheet that I made that only has the unique cities. The GeoNames API has a limit on the number of items (I think it is 30,000/day, 2,000 per hour), so instead of getting data for over 1200 rows, I have a list of about 520 places to get the latitude and longitude for. [The data are available in the course GitHub repo.](https://raw.githubusercontent.com/kristindawn/DC_OpenRefineTufts/gh-pages/files/Locs_to_GeoCode.csv) 

GeoNames is a great service, but you do have to sign up for a [free account to use the API](http://www.geonames.org/export/). 

One of the options in the `Edit column` menu is `Add column by fetching URLs...`. We are going to use this to take the column we just created and use it as the basis of a call to the GeoNames API. 

*NOTE:* API stands for application programming interface. I always have to look it up, so I thought I would include it here.

>## Demonstration
> 1. Click on the down arrow in the `City_State` column and choose `Edit column` > `Add column by fetching URLs...`.
> 2. Give the column a name of `GeoJSON`. This is going to be an intermediate column just for the GeoJSON data that is returned from GeoNames.
> 3. **THIS IS VERY IMPORTANT** Change the `Throttle delay` from the default `5000` milliseconds to `200` milliseconds. If you don't do this, it will only ask for a data from a new row every **5 seconds**, instead pf 5 rows every second.
> 4. Leave the `On error` on `set to blank`. GeoNames will also return its own errors.
> 5. The expression you need is: 
> ```'http://api.geonames.org/searchJSON?q='+escape(value, 'url')+'&country=&featureClass=P&continentCode=&username=**YOUR USER NAME HERE** &maxRows=1&featureCode='```
> 6. Click `OK` and wait.
>
{: .challenge}

You should get a set of data that looks like this:
``{"totalResultsCount":182,"geonames":[{"adminCode1":"CT","lng":"-72.92816","geonameId":4839366,"toponymName":"New Haven","countryId":"6252001","fcl":"P","population":130322,"countryCode":"US","name":"New Haven","fclName":"city, village,...","countryName":"United States","fcodeName":"populated place","adminName1":"Connecticut","lat":"41.30815","fcode":"PPL"}]}``

## Get the data you need from the JSON (Parse the JSON)

As you can see, the data from GeoNames is structured using JSON. This makes it easy to extract pieces from it using the language parsing capabilities in OpenRefine. This won't work for all kinds of structured data, but luckily JSON is on the list. You can find the functions in the GREL documentation on the [Other Functions](https://github.com/OpenRefine/OpenRefine/wiki/GREL-Other-Functions) page. 

> ## Demonstration
> 1. Click the down arrow in the GeoJSON column. Choose `Edit column` > `Add column based on this column`
> 2. Call the new column `Latitude`. Leave the options below that box as `set to blank`.
> 3. We are going to use the JSON parsing (`value.parseJson().???`) functionality to create an expression to just get the latitude, stored as `lat` in the column. To do this, we need to tell OpenRefine that we are looking at the first (and only) `geonames` JSON entry for the row and that we want the `lat`. What might this look like?
>
> > ## Solution
> > ```value.parseJson().geonames[0].lat```
> {: .solution}
>
> 4. Now you that you have the latitude, do the same thing for the longitude.
>
> > ## Solution
> > ```value.parseJson().geonames[0].lng```
> {: .solution}
>
{: .challenge}
