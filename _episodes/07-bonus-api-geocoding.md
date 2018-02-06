---
title: "Geocoding in OpenRefine using an API"
teaching: 10
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

Combining columns is not as intuitive as you might expect it to be. We are going to use what we learned about how OpenRefine understands what is in columns 

>## Exercise
>
> We are going to combine our cleaned up `City` and `State` data to create one column that we can use as the basis for our search using the GeoNames API. To concatenate strings in two columns, we can use the `+`. This also works for other text that we would like to add, which has to be put in `""`. 
>
> 1. Click on the down arrow in the `City` column and choose `Edit column` > `Add column based on this column`.
> 2. Give the new column the name `City_State`.
> 3. We want the text from the `City` column (value), the text from the `State` column, and a `, ` in between. Our expression is:
> >## Solution
> > ``value  + ", " + cells["State"].value``
> >{: .solution}
> 4. Leave the default `set to blank` if the process doesn't work. The preview should show `City, ST`. If it doesn't, check your expression.
> 5. Click `OK` 
>
{: .challenge}

