---
title: "Filtering and Sorting with OpenRefine"
teaching: 10
exercises: 5
questions:
- "How can we select only a subset of our data to work with?"
- "How can we sort our data?"
objectives:
- "Filter to a subset of rows by text filter or include/exclude."
- "Sort table by a column."
- "Sort by multiple columns."
keypoints:
- "OpenRefine provides a way to sort and filter data without affecting the raw data."
---

# Lesson

## Filtering

There are many entries in our data table. We can filter it to work on a subset of the data in the list for the next set of operations. Please ensure you perform this step to save time during the class.

1. Click the down arrow next to `State` > `Text filter`. A `State` facet will appear on the left margin.
2. Type in `.` and press return. There are 787 matching rows of the original 1261 rows (and these rows are selected for the subsequent steps). There are also only 29 Choices in the State Facet that shows the original text facet.
3. At the top, change the view to `Show` 50 `rows`. This way you will see as many matching rows as possible.

> ## Exercise
>
> 1. What states are selected by this procedure?  
> 2. Why didn't the Cluster we did in the last step catch some of these? 
> 
> > ## Solution
> > The states that are left either didn't have any matches and are just not formatted how we want, or they are shows that were cancelled. 
> > The states with the cancelled shows weren't caught because OpenRefine didn't see `Ill.` and `Ill., cancelled` as the same thing. 
> > There are only 4 examples with `cancelled`. Go ahead and edit the entry, removing the `,cancelled`. You should have 26 choices in the 
> > facet.
> > 
> {: .solution}
{: .challenge}

### Excluding entries


In addition to the solutions included above, another way to narrow our filter is to `include` and/or `exclude` entries in a facet. If you still have your facet for `State`, you can use it, or use drop-down menu > `Facet` > `Text facet` to create a new facet. Only the entries with names that agree with your `Text filter` will be included in this facet.

Faceting and filtering look very similar. A good distinction is that faceting gives you an overview description of all of the data that 
is currently selected, while filtering allows you to select a subset of your data for analysis. 


> ## Exercise
>
> Use `include / exclude` to select only entries from one of these two species.
>
> > ## Solution
> > 
> > 1. In the facet (left margin), click on one of the names, such as `D.T.`. Notice that when you click on the name, or hover
> > over it, there are entries to the right for `edit` and `include`. 
> > 2. Click `include`. This will explicitly include this species, and exclude others that are not expicitly included. Notice that the
> option now changes to `exclude`.
> > 3. Click `include` and `exclude` on the other species (`Me.`) and notice how the two entries appear and disappear
> >  from the table.
> > 
> {: .solution}
{: .challenge}

**PRO TIP:** You can clear all of the filters you have created in a facet using the `reset` in the top right corner of the box, right above the `Cluster` button.

## Sort

You can sort the data in a column by using the drop-down menu available in that column.
There you can sort by `text`, `numbers`, `dates` or `booleans` (`TRUE` or `FALSE` values). You can also specify what order to put `Blanks` and `Errors` in the sorted results.

If this is your first time sorting this table, then the drop-down menu for the selected column shows `Sort...`. Select what you would like to sort by (such as `numbers`). Additional options will then appear for you to fine-tune your sorting.


> ## Exercise
>
> Sort by State. What do you notice?
{: .challenge}

If you try to re-sort a column that you have already used, the drop-down menu changes slightly, to > `Sort` without the `...`, to remind you that you have already used this column. It will give you additional options:

* > `Sort` > `Sort...` - This option enables you to modify your original sort. 
* > `Sort` > `Reverse` - This option allows you to reverse the order of the sort.
* > `Sort` > `Remove sort` - This option allows you to undo your sort.

