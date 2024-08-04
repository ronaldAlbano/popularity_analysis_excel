-----

**Situation**

Social Buzz, a rapidly growing social media and content creation company founded in 2010, has reached over 500 million active users monthly and faces significant challenges in scaling their technology and preparing for an IPO. With a core team of 200 technical staff, they handle a large volume of unstructured data from over 100,000 daily content posts.

-----

**Task**

From the given dataset and data model, Social buzz wants us to determine the top 5 categories with the largest popularity for them to focus on in preparation for an IPO. To achieve this, our tasks are to:
- Identify which datasets will be required to answer the client’s business question.
- Clean the datasets and merge them to prepare the data for analysis.
- Determine the answer to the client’s business question.

-----

**Action**

The 7 datasets; user, profile, location, session, content, reaction, and reactiontypes. 

**The  Data Model**
<img src="https://i.imghippo.com/files/SNRK01722750945.png">

From this we've identified Reaction, Content, and Reaction Types as our relevant data sets.

To clarify why you made this selection:

The brief carefully it states that the client wanted to see “An analysis of their content categories showing the top 5 categories with the largest popularity”.
As explained in the data model, popularity is quantified by the “Score” given to each reaction type.
We therefore need data showing the content ID, category, content type, reaction type, and reaction score.
So, to figure out popularity, we’ll have to add up which content categories have the largest score.

But! Before we begin to work with the data sets, we’ll need to ensure that the data is clean and ready for analysis…

<img src="https://i.imghippo.com/files/HRuUr1722735824.png">


**Data Cleaning**

In Content File

Removed the URL column and the USER ID (as it is not necessary for quantitative analysis and our focus is the top 5 categories of content).
Checked for missing values using the filter.
Checked for duplicate values.
Found some values in the category containing quotes ("). Replaced the quotes using the find-and-replace function.
Renamed the column "type" to "Content Type" for more clarity.

In Reactions File

Removed the USER ID column.
Checked for missing values using the filter.
Found some missing values in the Reaction Type column. Deselect all values, then select only the blanks to remove all rows with missing values.
Checked for duplicate values
Renamed the column "type" to "Reaction type" for more clarity.

The provided Reaction Type File has already been cleaned.


**Data Modeling**

To identify the top 5 categories, we will create a final data set by merging your three tables together. The Reaction table will be our base table. First, join the relevant columns from your Content data set, and then from the Reaction Types data set using the VLOOKUP formula.

To get the Content Type values into the Reactions Table:

=VLOOKUP(B2, Content.csv!$B:$D, 2, FALSE)

To get the Category values into the Reactions Table:

=VLOOKUP(B2, Content.csv!$B:$D, 3, FALSE)

To get the Sentiment values into the Reactions Table:

=VLOOKUP(C2, ReactionTypes.csv!$B:$D, 2, FALSE)

To get the Score values into the Reactions Table:

=VLOOKUP(C2, ReactionTypes.csv!$B:$D, 3, FALSE)

Click the bottom right corner of a cell that contains the formula, and Excel will autofill the column down to the end of the adjacent column’s data.

Next, copy the 4 new columns and paste them as values only, so that the data remains intact even if changes occur to the other files.

Finally, rename the table to "Cleaned Table."

<img src="https://i.imghippo.com/files/51SGn1722741368.png">


**Data Analysis**

Figure out the Top 5 performing categories. Add up the total scores for each category using "Sum if" formula
<img src="https://i.imghippo.com/files/689WQ1722751554.png">

Create a New Sheet:

We created a new sheet named "Popular Categories."

Copy and Paste Category Column:

Copy and paste the Category column from the Cleaned Table into the "Popular Categories" sheet.
Go to the Data tab in Excel and use the "Remove Duplicates" feature to ensure only unique values are left.

Compute Aggregate Scores:

Use the SUMIF function to compute the aggregate scores for each category: =SUMIF('Cleaned Table'!F:F, 'Popular Categories'!A2, 'Cleaned Table'!H:H)

Autofill the Formula:

After calculating the first cell, autofill the formula down the column to compute scores for all categories.

Sort the Categories:

Sort the categories based on aggregate scores from largest to smallest.

Insert a Chart:

Insert a 2-D Clustered Bar chart.
Enhance the chart's settings and properties to clearly highlight the top 5 popular categories.



-----

**Results**

The content categories showing the top 5 largest popularity are Animals, Science, Healthy Eating, Technology, and Food. These are the areas where they can focus in preparation for their upcoming IPO.
