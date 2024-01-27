---
layout: default
title: Lab 1
nav_order: 1
parent: Lab Notebook
---
# Lab 1: Spreadsheets
## Acknowledgments
The inspiration for this lab is from [Lab 3](https://f20idh.ryancordell.org/2020/09/22/Data-and-Metadata/){:target="_blank"} of Ryan Cordell's Intro to DH course (F20).

## Helpful References and Tools for Working with Spreadsheet Data
- Jenn Riley, NISO, [“Understanding Metadata,”](https://groups.niso.org/higherlogic/ws/public/download/17446/Understanding%20Metadata.pdf){:target="_blank"}, especially pgs 1-18
- [WTFcsv](https://databasic.io/en/wtfcsv/){:target="_blank"}
- [Raw Graphs](https://app.rawgraphs.io/){:target="_blank"}
- [Breve](http://hdlab.stanford.edu/breve/){:target="_blank"}
- [Flourish](https://flourish.studio/){:target="_bank"}
- [Tableau](https://public.tableau.com/en-us/s/){:target="_blank"}
- [XLMiner Analysis Toolkit](https://workspace.google.com/marketplace/app/xlminer_analysis_toolpak/600284989882){:target="_blank"}

## Woo Hoo, Spreadsheets
Today we are going to explore the exciting world of spreadsheets. Spreadsheets are the form in which we often encounter historical or literary data, and so for this reason it's worth taking the time to think about the format itself, the kinds of questions we can ask of tabular data, and the skills we might need to answer those questions. We'll be keeping it very simple in this lab. I've included a list above of various free programs and platforms you can use to explore and visualize spreadsheet (or tabular) data, and these tools can be useful and are well worth exploring. However, in this lab we are going to focus on the affordances of Google sheets to think about how you can explore historical and literary data without having to use any additional tools (apart from Google sheets itself).

## One: An introduction to tabular data
We'll start in class with a discussion of an example of relatively straightforward and already cleaned historical data: data from the 1840 US Census. You can find this spreadsheet uploaded to our Canvas site (go to Files > labs > lab-1). We'll talk about how spreadsheets are organized, what the process of creating this spreadsheet might have looked like (see original reports [here](https://www.census.gov/library/publications/1841/dec/1840c.html){:target="_blank"}), and terms we will use in discussing them, including "csv/tsv," "metadata," and "controlled vocabulary."

We'll also look at this spreadsheet using one of the tools listed above: [view the 1840 Census on WTFcsv](https://databasic.io/en/wtfcsv/results/61d8a486da7d150900acd9e6?submit=true){:target="_blank"} and talk about wtf is happening here.

## Two: Explore the Trans-Atlantic Slave Trade Dataset
Then we'll move on to another example, one from our reading for next week: the [Trans-Atlantic Slave Trade Database](https://www.slavevoyages.org/voyage/database){:target="_blank"}. We'll examine a downloaded spreadsheet of the data and discuss how we can use pivot tables to do initial explorations of large datasets.

We'll go through this together in class, but here's what you'll do:
1. Download the Trans-Atlantic Slave Trade Database spreadsheet from Canvas. I've placed a copy of this spreadsheet in the lab 1 folder on Canvas (Files > labs > lab-1). The filename is "trans-atlantic-slave-trade.xlsx".
2. Then upload this spreadsheet to the Google drive folder you created and shared with me by today's class and open the spreadsheet using Google sheets (right/control-click on the file in Google drive, and select Open with > Google Sheets). Once the spreadsheet is open, go to File > Save as Google Sheets to save a Google sheets copy of the spreadsheet file in your Google drive folder.
3. We'll talk through the composition of this spreadsheet in class. Then, we will create a pivot table that displays the number of voyages per year using the "Year of arrival at port of disembarkation" metadata field. I'll walk us through how to do this in class, but you can also read [these instructions](https://support.google.com/a/users/answer/9308944?hl=en){:target="_blank"} (choosing to insert the pivot table in a "New Sheet" will create a new tab in your spreadsheet where the pivot table will go).
4. We will talk about how to order this table by year and by number of voyages, and we'll create a line chart showing the number of voyages per year (x axis = year, y axis = number of voyages).
5. We will then create pivot tables displaying the counts for the following metadata fields:
    - Particular outcome of voyage
    - Outcome of voyage for slaves
    - African resistance

## Three: Explore Post45 HathiTrust data
Finally, we'll explore a dataset of metadata for fiction held by the [HathiTrust digital library](https://www.hathitrust.org/){:target="_blank"} from 1945 to 2000. This dataset is a subset of a dataset compiled by the [Post45 Data Collective](https://data.post45.org/hathitrust-post45-fiction/){:target="_blank"} (theirs includes data through the early 2010s; I made a slightly smaller version for us to work with in class). You can find an [online version of this dataset on the Post45 Data Collective website](https://view.data.post45.org/index){:target="_blank"} (this is where I downloaded the data); this page is also where to look for metadata field descriptions (click on the question mark next to each column name).

Here's what you'll do:
1. First, as you did with the Trans-Atlantic Slave Trade spreadsheet, you should download the Post45 HathiTrust dataset from Canvas. (Files > labs > lab-1). The filename is "post45-hathitrust-fiction-1945.xlsx". Then, upload this file to your Google drive folder, open it with Google sheets, and save a Google sheets version.
2. Explore the dataset's metadata fields and their descriptions using [this page](https://view.data.post45.org/index){:target="_blank"}.
3. Create 2 pivot tables displaying summaries of 2 different metadata fields and/or answering 2 different questions about this dataset. For example, you might wonder how many works are tagged as particular genres, or how many works in the dataset were actually initially published prior to 1945 (for this one, you would need to think about the several different date columns included in this spreadsheet and what they each mean). You may also wish to visualize the totals listed in your pivot table by inserting a chart.
    - 3.a Alternatively, you may use one of the tools listed above for visualizing spreadsheet data (WTFcsv, Raw Graphs, Breve, Flourish, Tableau) to visualize the Post45 HathiTrust data in some way that provides answers to 2 different questions about this dataset. If you have the skills, you may also choose to create a Jupyter notebook or R notebook that visualizes this data in some way that provides answers to 2 different questions about the dataset. I think these are the more challenging routes, but if you are interested in exploring some of these data visualization platforms and tools or in working on your data visualization skills in Python or R, you may choose to try it. This may involve googling around to find instructions and/or tutorials about how to use these tools.

## Lab Notebook Entry
### Due:
- By class on Wed, Feb 7

Your lab notebook can take the form of one continuous Google doc, or you may choose to create individual doc files for each lab notebook entry.

In your lab notebook entry for lab 1, you should include the following things:
1. Links to your personal Google sheet copies of the Trans-Atlantic Slave Trade dataset and the Post45 HathiTrust dataset. These sheets should also be included in your shared Google drive folder somewhere.
2. At least one thing you observed or learned from your exploration of the Post45 HathiTrust dataset. This can be something odd or unexpected, something that confused you, something that initially confused you but that you figured out, etc.
3. A response to this prompt: Our readings for week 3 focus on the affordances and limitations of quantification and objectivity. What do the spreadsheets we explored in lab 1 make it possible to know or to study or to question, and what do they occlude or make impossible to know or to study or to question? You may use any spreadsheet or any combination of spreadsheets we discussed in this lab 1 and any reading or combination of readings from week 3, but your notebook entry should include discussions of at least one specific spreadsheet in connection to at least one of our readings from week 3. This discussion should be specific but it needn't be long (i.e., 2-4 paragraphs).
