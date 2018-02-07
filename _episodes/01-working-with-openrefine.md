---
title: "Working with OpenRefine"
teaching: 10
exercises: 10
questions:
- "How can we bring our data into OpenRefine?"
- "How can we sort and summarize our data?"
- "How can we find and correct errors in our raw data?"
objectives:
- "Create a new OpenRefine project from a CSV file on the web."
- "Recall what facets are and how they are used to sort and summarize data."
- "Recall what clustering is and how it is applied to group and edit typos."
- "Manipulate data using previous steps with undo/redo."
- "Employ drop-downs to split values from one column into multiple columns."
- "Employ drop-downs to remove white spaces from cells."
keypoints:
- "Faceting and clustering approaches can identify errors or outliers in data."
---

# Lesson

## Creating a Project


Start the program. (Double-click on the openrefine.exe file (the icon looks like a diamond). Java services will start on your machine, and OpenRefine will open in your browser).

Launch OpenRefine (see [Getting Started with OpenRefine](http://www.datacarpentry.org/OpenRefine-ecology-lesson/00-getting-started/)).

OpenRefine can import a variety of file types, including tab separated (`tsv`), comma separated (`csv`), Excel (`xls`, `xlsx`), JSON, XML, RDF as XML, Google Spreadsheets. See the [OpenRefine Importers page](https://github.com/OpenRefine/OpenRefine/wiki/Importers) for more information.

In this first step, we'll browse our computer to the sample data file for this lesson. In this case, I have partially cleaned up a very simple dataset of Barnum and London Circus stops from 1881-1890. The original data I used can be found on the [Circus Historical Society Barnum Route from 1881-1890 page](http://www.circushistory.org/Routes/PTB1881.htm).

Instead of downloading the data, we are going to grab it straight from the CSV file that I put in my GitHub repository for this workshop. You can get a [preview of the data](https://github.com/kristindawn/DC_OpenRefineTufts/blob/gh-pages/files/PTB1881_wyear.csv) in GitHub. Take a look and see if you notice anything specific about the data. When you are ready, the URL for the dataset that we are going to copy into OpenRefine is: ```https://raw.githubusercontent.com/kristindawn/DC_OpenRefineTufts/gh-pages/files/PTB1881_wyear.csv```


Once OpenRefine is launched in your browser, the left margin has options to `Create Project`, `Open Project`, or `Import Project`. Here we will create a new project:

1. click `Create Project` and select `Get data from` `Web Addresses (URLs)`. This won't work for all URLs, but you can always test it and see.  
2. Click `Next>>` under the browse button to upload the data into OpenRefine.  
3. OpenRefine gives you a preview - a chance to show you it understood the file. If, for example, your file was really tab-delimited, the preview might look strange, you would choose the correct separator in the box shown and click `Update Preview` (bottom left). If this is the wrong file, click `<<Start Over` (upper left).  
4. If all looks well, change the `Project name` at the top to `PTB1881-1890`. Click `Create Project>>` (upper right next to the `Project name` box). 

Note that at step 1, you could upload data from a file on your computer. The rest of the steps are the same.

## Faceting

*Exploring data by applying multiple filters*

OpenRefine supports faceted browsing as a mechanism for

* seeing a big picture of your data, and
* filtering down to just the subset of rows that you want to change in bulk.

Typically, you create a facet on a particular column. The facet summarizes the cells in that column to give you a big picture of that column, and allows you to filter to some subset of rows for which the cells in that column satisfy some constraint. That's a bit abstract, so let's jump into some examples. 

[More on faceting](https://github.com/OpenRefine/OpenRefine/wiki/Faceting)

Here we will use faceting to look for potential errors in data entry in the `Month` column.

1. Scroll over to the `Month` column.
2. Click the down arrow and choose `Facet` > `Text facet`.
3. In the left panel, you'll now see a box containing every unique value in the `Month` column 
along with a number representing how many times that value occurs in the column.
4. Try sorting this facet by name and by count. Do you notice any problems with the data? What are they?
5. Hover the mouse over one of the names in the `Facet` list. You should see that you have an `edit` function available. 
6. You could use this to fix an error immediately, and OpenRefine will ask whether you want to make the same correction to every value it finds like that one. Since there aren't too many errors here, you can go ahead an fix the errors you find. 

>## Solution
>
> There will be one year where June is incorrectly abbreviated as Jun and one misspelling of October. In the end, there should be 8 months >in the facet - April through November.   
{: .solution}

>## Exercise
>
> 1. Using faceting, look at the YEAR column.  
> 2. Is the column formatted as Number, Date, or Text? How does changing the format change the faceting display?
> 3. Which years have the most and least observations?
>
> > ## Solution
> > 
> > 1. For the column `YEAR` do `Facet` > `Text facet`. A box will appear in the left panel showing that there are 10 unique entries in
> > this column.  
> > 2. By default, the column `YEAR` is formatted as Text - you can tell this by the fact that the values are in black. You can change the 
> >format by doing `Edit cells` > `Common transforms` > `To number`. Doing `Facet` > `Numeric facet` creates a box in the left panel that
> >shows a histogram of the number of entries per year. Notice that the data is shown as a number, not a date.
> >DO NOT DO THIS BUT: If you instead transform the column to a date, the program will assume all entries are on January 1st of the year.   
> > 3. After creating a facet, click `Sort by count` in the facet box. The year with the most observations is 1997. The least is 1977. 
> > 
> {: .solution}
{: .challenge}

## Split
*Creating multiple columns from one based on a particular character*

If data in a column needs to be split into multiple columns, and the parts are separated by a common separator (say a comma or a space), you can use that separator to divide up the pieces into their own columns.


1. We want to split the `Route Date` column into separate colums for the date and the location using the space after the date as the separator. 

**What could go wrong with this?** 

>## Solution
> Some of the place names, like "New York" have a space in the name of the city. If we let OpenRefine split it _without_ indicating how many >columns we want, it will split it as many times as it can. Since we know we only want it to split it into two columns, the date and the >place, we can indicated that before we ask it to split it.
{: .solution}

2. Click the down arrow at the top of the `Route Date` column. Choose `Edit Column` > `Split into several columns...`
3. In the pop-up, in the `Separator` box, replace the comma with a space. 
4. Where it says `Split into`, type in 2; this will limit the number of columns to 2 instead of as many as OpenRefine can make.
5. **Uncheck the box that says `Remove this column`.** This will leave the original column. It is always good to have this information to go back to.
6. Click `OK`. You'll get two new columns called `Route Date 1` and `Route Date 2`. 

**What do you notice about the new columns?**

7. Click on the down arrow for each of the new columns, choose `Edit column` > `Rename Column`. Name the columns with the dates `Date` and the columns with the cities `Location`.
8. Repeat this process for the new `Location` column to split the city and State. This will help us clean up the list, as most of the incosistencies exist with the way that the states have been entered.

**PRO TIP:** If you can use a standard way of representing something, do it. In this case, we will be using the International Standards Organization (ISO) Standard for the 2 letter state codes. This sounds intense, but you can find all of the [information on Wikipedia](https://en.wikipedia.org/wiki/ISO_3166-2:US) and you will find that they are very familiar. Using a standard like this will make it easier for others to use your data. 

## Clustering

In OpenRefine, clustering means "finding groups of different values that might be alternative representations of the same thing". For example, the two strings `New York` and `new york` are very likely to refer to the same concept and just have capitalization differences. Likewise, `Gödel` and `Godel` probably refer to the same person. Clustering is a very powerful tool for cleaning datasets which contain misspelled or mistyped entries. OpenRefine has several clustering algorithms built in. Experiment with them, and learn more about these algorithms and how they work. 

1. In the `Location` Text Facet we created in the step above, click the `Cluster` button.
2. In the resulting pop-up window, you can change the `Method` and the `Keying Function`. Try different combinations to 
 see what different mergers of values are suggested.
3. Select the `key collision` method and `fingerprint` keying function. It should identify eight clusters. 
4. Go through the list, putting the ISO two-letter code for each state in the `New Cell Value`. Click the `Merge?` box beside each one.
5. Click `Merge Selected and Recluster` to apply the corrections to the dataset.
6. Try selecting different `Methods` and `Keying Functions` again, to see what new merges are suggested. You may find there are 
 still improvements that can be made, but don't `Merge` again; just `Close` when you're done.  We'll now 
 see other operations that will help us detect and correct the remaining problems, and that have other, more general uses.

Important: If you `Merge` using a different method or keying function, or more times than described in the instructions above, 
your solutions for later exercises will not be the same as shown in those exercise solutions.

[More on clustering](https://github.com/OpenRefine/OpenRefine/wiki/Clustering-In-Depth)



## Undo / Redo

It's common while exploring and cleaning a dataset to discover after you've made a change that you really should have done something else first. OpenRefine provides `Undo` and `Redo` operations to make this easy. We are not going to do this right now, but if you want to try it later you can use the steps in the Solution below.

>## Solution
>
>1. Click where it says `Undo / Redo` on the left side of the screen. All the changes you have made so far are listed here.
>2. Click on the step that you want to go back to, in this case the previous step. The added columns will disappear.
>3. Notice that you can still click on the last step and make the columns reappear, and toggle back and forth between these states.
{: .solution}
