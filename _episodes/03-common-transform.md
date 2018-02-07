---
title: "Common Transforms and Transforms"
teaching: 10
exercises: 15
questions:
- "What are the common transforms and how can they help us?"
- "How can common transforms help us find and correct common errors."
- "How can I edit multiple rows at once using transforms?"
objectives:
- "Use some of the common transforms to try and creat consistency in our data."
- "Investigate writing our own transforms with external resources."
- "Use the history in transforms to make our lives easier."
- "Manipulate data using previous steps with undo/redo."
keypoints:
- "Transforms, common or written by us, are a powerful way to edit lots of data at once."
---

# Lesson

## Common Transforms.

### Whitespace

Words with spaces at the beginning, end, or with consecutive spaces in the middle, are particularly hard for we humans to tell from strings without, but the blank characters will make a difference to the computer. We usually want to remove these. OpenRefine provides a tool to remove blank characters from the beginning and end, `Trim leading and trailing whitespace`, and multliple spaces in the middle,`Collapse consecutive whitespace` of any entries that have them. We don't have any of these in this exercise, but it is a useful tool to know about.  

>## Optional Exercise
> 1. In the header for the column `City`, choose `Edit cells` > `Common transforms` > `Trim leading and trailing whitespace`.
> 2. It will show that there were 0 columns edited. It does not hurt to do this as a general step in your data cleanup, as it could save you a > lot of grief later.
{: .challenge}


### Case

Case matters in OpenRefine, and this can cause problems when you have messy data with lots of inconsistencies. OpenRefine offer you three options in the common tranforms to chance the case of entire columns of data; `To titlecase`, `To uppercase`, and `To lowercase`. 

Titlecase is probably the least commonly used, and will capitalize each word. To uppercase and to lowercase change text to all capitals or all lowercase.

>## Exercise
> We are going to use the `To uppercase` to make all of the states all capitals.
> 1. Click on the down arrow in the `State` column heading. Choose `Edit cells` > `Common transforms` > `To uppercase`.
> 2. What do you notice about the faceted list of states? Did anything change? It is fine if nothing did.
{: .challenge}

## Transforms

In addition to the common transforms that OpenRefine has provided, you can also write short expressions using the Google Refine Expression Language (or GREL). We will use transforms to keep cleaning up the `State` field.

We will be focusing on the `String Functions`, which are outline in the [GREL documentation](https://github.com/OpenRefine/OpenRefine/wiki/GREL-String-Functions). There are also functions for the other data types, including `Math`, `Date`, and `Boolean` data (just to name a few).

A few tips for using the `Edit cells` > `Transform...` window:

* The "value" is the data in the column that you opened the transform from. 
* Data from other columns can be included in an expression using: `cells["COLUMN NAME"].value`.
* The preview is key to identifying possible problems. It only shows an example of the data, but you should be able to get a sense of whether the result is what you want.
* The `History` tab will become your best friend. It allows you to reuse expressions that you have used in your OpenRefine environment, regardless of the project.

>## Exercise
> We are going to get rid of all of the `.` in the state column by replacing them with nothing.
> 1. Click on the down arrow in the `State` column, choose `Edit cells` > `Transform...`.
> 2. In the Transform window, make sure that the `Language` is set to `Google Refine Expression Language (GREL)`. You can also use Python/Jython or Clojure, but today we will use GREL. 
> 3. Currently, the `Preview` of the data looks like the original data; this will change as we right our expression.
> 4. We are going to use the `replace` function to remove the `.`s. Replace needs 3 strings to work: the input (in our case this will be `value`), the string to be replaced (`"."`), and the string you want replace it with (`""`). So, our full expression will be: ``replace(value, ".", "")``
> 5. Make sure that the preview matches what you expect (example `D.T.` becomes `DT`). The `On error` should be set to `keep original` to reduce the need to bring together columns later.
> 6. Click `OK`. 
{: .challenge}

To clean up the rest of the list, please just go through the list and manually edit the `State` column until all of the states have their two letter code. Are there any codes there that give you trouble?

