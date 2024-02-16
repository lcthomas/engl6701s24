---
layout: default
title: Lab 5
nav_order: 5
parent: Lab Notebook
---
# Lab 5: Web Scraping with Python
To access the notebook we are using for today's lab, follow the first link below. Loading the notebook may take a few minutes; this is normal. The second link is for the lab's GitHub repository.
- [Lab 5 Jupyter Notebook](https://mybinder.org/v2/gh/lcthomas/engl6701s24-lab5/HEAD?urlpath=lab%2Ftree%2Flab5.ipynb){:target="_blank"}
- [Lab 5 GitHub repository](https://github.com/lcthomas/engl6701s24-lab5){:target="_blank"}

## Acknowledgments
I have drawn from Melanie Walsh's [*Introduction to Cultural Analytics & Python* online textbook](https://melaniewalsh.github.io/Intro-Cultural-Analytics/welcome.html){:target="_blank"} in creating this lab.

## Running Jupyter Notebook on Your Own Computer
This is optional!

But if you're interested in running this notebook on your own computer, rather than relying on Binder, you can follow the instructions on [this page](https://melaniewalsh.github.io/Intro-Cultural-Analytics/02-Python/01-Install-Python.html){:target="_blank"} from Melanie Walsh's *Introduction to Cultural Analytics & Python*.

Then, head to [this lab's GitHub repository](https://github.com/lcthomas/engl6701s24-lab5){:target="_blank"} and download this notebook file (`lab5.ipynb`). You can then launch Jupyter Notebook (or JupyterLab) from within Anaconda, navigate to where you saved this notebook file, and open it on your own computer. If you elect to go this route, you won't need to create a save a notes document for this lab; instead, you can enter code directly into your own copy of the notebook. Then, once you've completed the lab, move a copy of the notebook into the Google drive folder you shared with me, where I can download it.

To ensure this notebook works on your computer, you will need to make sure you have installed the following packages (I think all of them come with Anaconda, if you followed Walsh's directions linked above):
- pandas
- requests
- beautifulsoup4
- time
- re

## Research Context of Today's Lab
Web scraping is a very useful skill for the purposes of data collection. If you understand the basics of web scraping, you can begin to gather information in a programmatic way from almost any website. Today's lab was inspired by Melanie Walsh's and Maria Antoniak's article [“The Goodreads ‘Classics’: A Computational Study of Readers, Amazon, and Crowdsourced Amateur Criticism"](https://culturalanalytics.org/article/22221-the-goodreads-classics-a-computational-study-of-readers-amazon-and-crowdsourced-amateur-criticism){:target="_blank"}, which we will read in week 12.

To write their article, Walsh and Antoniak scraped data about books shelved as "classics" on [Goodreads](https://www.goodreads.com/){:target="_blank"}, as well as over 127,000 Goodreads reviews of these books. To collect this data, they created a scraper, which they uploaded to GitHub upon publication of their article so that others could use their code. You can find the scraper here: <https://github.com/maria-antoniak/goodreads-scraper>.

In today's lab, you will learn about web scraping, practice scraping some simple web pages, and then, following in some of Walsh's and Antoniak's footsteps, learn about how to collect information about books shelved as "classics" on Goodreads.

Note: since the publication of Walsh's and Antoniak's article in 2021, Goodreads has changed much about how they organize their site and display search results, reviews, and information about books. These changes have broken many aspects of Walsh's and Antoniak's scraper. This is a common issue with web scraping. While non-functional or outdated code can still be very useful in helping you understand how to scrape data from a particular site, it is best to use the most recent repositories or example code you can find.

## Interested in Leveling This Lab Up?
If you'd like more practice with web scraping after completing this week's lab, you might be interested in trying to scrape a review -- or a collection of reviews -- from Goodreads. In other words, you could write your own Goodreads review scraper (or part of one, or try to write one). You might start by investigating how Walsh and Antoniak solved this problem back in 2021 by digging around in [their Goodreads scraper repo](https://github.com/maria-antoniak/goodreads-scraper).

## Lab Notebook Entry
Due:
- By class on Wed, March 6

In your lab notebook entry for this week, you should include the following things:
1. Responses to questions 1-6 from the Lab 5 Jupyter notebook.
2. A response to **one** of the following prompts:
    - Discuss your experience exploring Python in this week's lab in relation to at least one of our readings assigned for next week (week 7). This discussion should be specific but it needn't be long (i.e., 2-4 paragraphs).
    - Write a response to at least one of our readings assigned for next week (week 7). The topic is up to you. Your response should be specific but it needn't be long (i.e., 2-4 paragraphs).
3. The dataset you plan to use in completing [Lab 6](https://lindsaythomas.net/engl6701s24/labs/lab-6.html/){:target="_blank"}. This means you should read through the [Lab 6](https://lindsaythomas.net/engl6701s24/labs/lab-6.html/){:target="_blank"} assignment page before you make your selection. Please include a link to the dataset.
