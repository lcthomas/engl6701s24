---
layout: default
title: Lab 2
nav_order: 2
parent: Lab Notebook
---
# Lab 2: Regular Expressions
## Acknowledgments
In creating this lab, I have lightly adapted [Lab 4](https://f20idh.ryancordell.org/2020/09/30/CleaningData/){:target="_blank"} from Ryan Cordell's Intro to DH course (F20).

## RegEx Resources
- Doug Knox’s [“Understanding Regular Expressions”](https://programminghistorian.org/en/lessons/understanding-regular-expressions){:target="_blank"} tutorial at the Programming Historian provides a nice introduction into the basics of regex for cleaning historical data.
- This [Regular Expressions Quick Start](https://www.regular-expressions.info/quickstart.html){:target="_blank"} gives a useful overview of the core regex you’ll need for today’s work, and the larger resource delves into details for the future.
- Once you understand the basics of regex matching, [this cheat sheet](http://web.mit.edu/hackl/www/lab/turkshop/slides/regex-cheatsheet.pdf){:target="_blank"} may help you recall precisely the characters you need for particular patterns.
- See the "Basic Search-Replace Options" section at the bottom of this page.

## Introduction
The readings in week 4 focus on collecting, organizing, and cleaning data. If you want to analyze data in aggregate, you may decide you want to normalize some categories or correct errors in data collection. [Katie Rawson and Trevor Muñoz helpfully complicate this impulse](https://dhdebates.gc.cuny.edu/read/untitled-f2acf72c-a469-49d8-be35-67f9ac1e3a60/section/07154de9-4903-428e-9c61-7a92a6f22e51){:target="_blank"}, and so while lab 2 focuses on learning the basics of one strategy for cleaning data, we’ll also be thinking in our class discussion about how to decide to clean or not to clean (or something in between) your data.

We will be learning about regular expressions (regex) today using the online resource [RegEx 101](https://regex101.com/){:target="_blank"}, which allows you to test expressions and breaks down precisely what they’re doing in the Explanation and Match Information panels. It also includes a Quick Reference panel (bottom right), which allows you to search for and select the specific regular expressions you need.

We will be dealing with arcane and abstract syntax today. Regex is very powerful and precise, but because of this, it's also very fiddly, and sometimes crafting the regular expression you need to solve a problem or complete a task is a frustrating process of trial and error that can take awhile, especially when you are first learning. I don’t use regex every day, and so I don’t have its intricacies memorized. Typically I will use regex when faced with a problem that requires me to standardize some aspect of a dataset. When I encounter those problems, however, I typically need to refer to a regex guide to remind myself precisely what symbols translate to what textual patterns. Which is to say: you don’t need to memorize regex syntax in order to find it useful. What’s most essential is that you are able to identify what kinds of problems regex might help you work through.

**A note about terminology:** The term "regex" names a generalizable function, not necessarily a specific platform, program, or tool. Today we are focusing on regex as its implemented in RegEx 101, but you can conduct searches using regex across multiple platforms, including Google sheets, Microsoft Word, in Python, in R, etc. While the general principle remains the same across platforms and languages, different applications of regex often have slightly different syntaxes or rules governing its use within that platform or language.

## What are Regular Expressions?
In brief, regular expressions provide a way to abstractly describe the structure of texts. Using regex, you can specify patterns that will allow you to quickly make changes across a dataset, rather than correcting data line by line or instance by instance. Regex is not tied to a particular tool or platform. You can use regex in most programming languages (though the specific syntax will vary slightly), as well as in the “search and replace” functions of many spreadsheet or database applications or word processors. While these days I frequently use regex when normalizing or cleaning data using Python, before I learned anything about Python, I first learned how to utilize regular expressions by cleaning a large dataset using [BBEdit's regex find and replace features](https://methodshop.com/bbedit-grep/){:target="_blank"} (or "GREP"). I will still sometimes use BBEdit for data cleaning, just because I'm faster at regex using this program than I am with Python (BBEdit uses [PCRE regex syntax](https://www.php.net/manual/en/reference.pcre.pattern.syntax.php){:target="_blank"}; Python's regex syntax is a little different). In other words, having a general understanding of regex is a portable skill that can prove useful in a variety of ways as you move into work with data.

So what does it mean to “abstractly describe the structure of texts?” Well, let’s say I have a large spreadsheet full of email addresses from different domains, providers, etc. (e.g. lindsaycthomas@miami.edu, l.thomas@cornell.org, lindsay_thomas@gmail.com). These email addresses are located in a "Contact Information" column along with phone numbers and addresses. I want to isolate all of the email addresses in my dataset and move them to their own "Email" column. I could do this using copy and paste, of course, but if my spreadsheet has hundreds or thousands of records (or rows), that could take awhile. Regex allows me to identify every email address in my spreadsheet based on its abstract structure, *regardless of the specific characters that comprise that email address*. Once identified, I can then also use the search and replace function on a spreadsheet program like Google sheets to effectively copy and paste each email address into its own column in my spreadsheet -- all in a matter of seconds (once I have crafted the regular expressions I need, that is). In this way, regex is about recognizing and taking advantage of the formal or textual features or patterns that occur *across* each record in your dataset to save time during the data cleaning process.

 For example, on a formal level, the following features or patterns describe an email address:

- a series of upper- and/or lower-case letters, digits, or symbols (from a set of allowed characters, though sometimes this may include a period)
- an @ symbol
- another series of upper- and/or lower-case letters, digits, or symbols
- a period
- a series of three letters following the period

In fact, this only describes US-based email addresses, as those from other countries can have longer suffixes (e.g. `.co.uk`), but this gives you a sense of how you might outline the abstract structure of text strings that we would recognize as email address.

## One: Testing regex on emails
The following regular expression encapsulates the above description of the abstract structure of a US email address:

`([A-Za-z0-9._%+-]+)@([A-Za-z0-9-]+)\.([A-Za-z]{2,4})`

To understand what this is doing, let’s use [Regular Expressions 101](https://regex101.com/){:target="_blank"}. First, make sure that, in the "Flavor" box on the left, you select `PCRE (PHP < 7.3)`. This means we will be using Perl Compatible Regular Expressions in today's lab (this is an older regex syntax based on the programming language perl; it is what BBEdit uses). In the “Test String” box, copy and paste the following:

```
testemail@gmail.com
test.email@gmail.com
test_email@gmail.com
testemail@mail.co.uk
```
Then, copy and paste the email regex above into the "Regular Expression" box. What worked, and what didn't? Why? We will walk through how this matching happens and discuss any that don’t work together. We’ll also experiment with some other regex that accomplish the same task:

`([A-Za-z0-9._%+-]+)@([A-Za-z0-9-]+)\.([A-Za-z.]+)`<br/>
`(.*)@(.*)\.(.*)`

We'll also talk about using regex to make substitutions, replacing each instance of `gmail` in our data with `hotmail`, and then replacing each suffix after the final period with `.org`.

## Two: Normalizing data
Next, we'll discuss how we might use regex to normalize data. We'll examine the [Post45 HathiTrust Fiction](https://view.data.post45.org/index) dataset from last week. Specifically, we will talk about how the authors of this dataset might have used regex to create the `shorttitle` metadata field using information in the `title` field. We'll also take a look at the text of [WEB Du Bois's *The Souls of Black Folk* on Project Gutenberg](https://www.gutenberg.org/files/408/408-0.txt){:target="_blank"} and discuss how we could use regex to prepare this text for analysis.

## Three: Cleaning data
Finally, we'll think about how to approach cleaning a dataset using regex. We will focus on the `pub` field from a small sample of [WhatEvery1Says](https://we1s.ucsb.edu/){:target="blank"} (WE1S) newspaper and magazine data. This is data that WE1S scraped from ProQuest Ethnic Newswatch and GenderWatch news databases. The sample below is taken from the `pub` column in a dataset of just under 1,000 records; I've only given you one instance of each title below, but each of these titles repeats at least 10-15 times throughout the entire dataset. The spreadsheet is in `.csv` format. Here's the data:

```
The Epoch Times New York ed.; New York (NY)
"La Voz Bilingüe"; Denver, Colo.
Jewish Advocate; Boston
Washington Informer; Washington, [D.C.]
News from Indian Country; Hayward, WI.?
Afro - American, 5 Star edition; Baltimore, Md.
Diverse Issues in Higher Education; Fairfax Virginia
The Gay &amp; Lesbian Review Worldwide; Boston, MA
"The Hispanic Outlook in Higher Education; [Paramus N.J
```

Here is the problem: As we can see, the `pub` column in this data includes not only the publication title, but also the city and (usually) US state where the newspaper or magazine is published. Instead of including the city and state in the `pub` column, we want to move the city and state to their own separate column and standardize the states to their two-letter abbreviations. We also want to eliminate all punctuation in both columns.

Our goal is to figure out what regex would convert these titles into a standard pattern: publication title in one column, and city and two-letter state abbreviation in another. Remember, we also want to eliminate all punctuation in both columns (though not necessarily *between* columns, as this file is in `.csv` format -- think about how those files are organized). On our Canvas site, you can find small file titled "regex-goal.csv" in the lab 2 folder (Files > labs > lab-2) that shows you what the goal format is for this exercise. Your task is to try to reproduce the contents and format of this file using regular expressions.

With such a diverse set of patterns, we probably can’t write a single regex that would convert them all in one fell swoop. But within the actual dataset there are many examples of each of these titles and patterns, so it would be to our benefit to develop several regex that will help us clean the data in a few steps rather than line by line.

As you work, you’ll want to consider:

- What consistent textual patterns can you describe abstractly in each line, and perhaps between lines?
- What steps would you need to follow—and in what order—to convert these values into two columns with the publication name in column one and the city and two-letter state abbreviation in column two? Remember: this data is taken from a `.csv` file. What column separator should you use?
- Are there any aspects of the text you cannot describe through regex and might therefore require hand cleaning?

We will use [RegEx 101's](https://regex101.com/){:target="_blank"} Substitution function to work on this. As you are completing the below exercise, **make sure to take note of every regular expression you use, and what that expression does (or its output) in a separate notes document. You will need this document for writing your lab notebook entry for this week.**

Here's how to get started:

1. To enable the substitution function, select "Substitution" in the Function panel on the left side of the screen. The regex portion of your screen should now be split in two: You should now see two "Substitution" boxes below the "Test String" box (one for the replacement value and one for the output). The output box is where the outcome of your regex will display.
2. To begin, copy and paste the publication and location data above to the "Test String" box. You should then see that same data appear in the "Substitution" box. The data in the "Substitution" box is the same as the data in the "Test String" box because we haven't made any changes to it yet.
3. Next, we need to select one abstract feature of the test string data to work on. Let's begin with an easy one: we want to delete all quotation marks. In the "Regular Expression" box, craft a regex that will identify all quotation marks in the test string data (this is not a trick; it's very easy). You should now see all quotation marks highlighted in the "Test String" box.
4. Here's where things get slightly trickier: next, you need to identify what to substitute for all quotation marks in the test string data. In this case, we want to substitute *nothing* for quotation marks because we want to delete them. So, keeping the top "Substitution" box blank (where it says "insert your replacement value here"), what do you notice about the output data below? Where have the quotation marks gone? What if, instead of substituting nothing for all quotation marks, you instead substituted a tab character (`\t`)? Or a comma? If you do this, what do you notice about the output? This is how the substitution function works: you craft a regex that *identifies* a particular abstract pattern, then you craft another regex that *substitutes* what you want to replace the pattern you have identified above with (this is really where groups and group substitution syntax comes in handy).
5. Making sure that you are replacing the quotation marks in the test string data with nothing, copy the output and paste that output into the "Test String" box. This is now our new input. Make sure to take note of what regular expression you used and what that regex did to your data in  your notes document.
6. Your task is then to craft as many regex's as you need to complete our goal: we want all publication titles in one column, we want city and two-letter state abbreviations in another, and we want to eliminate all punctuation within both columns. Make sure to take note of each regex you use and its output/what it does to the data in your notes document.

**Alternate lab for those who want to level up**
Instead of working within [RegEx 101](https://regex101.com/){:target="_blank"}, you could work with regular expressions in Python or R. Complete the same task as described above, but do it in a Jupyter notebook or an R notebook.

## Lab Notebook Entry
### Due:
- By class on Wed, Feb 14

In your lab notebook entry for this week, you should include the following things:
1. The regex's used to clean the data in step three above (or, if you just couldn't reach the goal, to come as near as you could get to our goal). There is no one right answer here; a variety of regex sequences will work. What I'm looking for is a good-faith effort.
2. A response to the following prompt: Discuss your experience working with regular expressions in this week's lab in relation to at least one of our readings assigned for week 4. This discussion should be specific but it needn't be long (i.e., 2-4 paragraphs).

---

## Basic Search-Replace Operations
The following guide to basic regex operators was adapted from Cordell's lab, which itself is an adaptation of Ben Schmidt’s RegEx exercise in his 2015 Humanities Data Analysis Course.

### Basic Operators
`*`, `?` and `+`

- `*` matches the preceding character **any number of times**, including no times at all.
- `+` matches the preceding expression **at least one time**.
- `?` matches the preceding expression exactly **zero or one times**.

`[]`

You can use brackets to indicate a range of characters, as in the email address example above. The regex in the first bracket (`[A-Za-z0-9._%+-]`) refers to any alphanumeric character as well as the following punctuation marks: ., %, +, -. You can also use brackets to extend more functionality to your search. Suppose you are searching through the Schmidt family records, but learn that 18th century families often spelled the name “Schmitt.” The regular expression `Schmi[td]t` would match either spelling (because in using this regex, you are saying that either a `t` or a `d` can go in that place).

`()`

Parenthesis let you group a set of characters together. That is useful with replacements, described below: but it also lets you apply the operators above to groups of words. So suppose you have a document full of references to John Quincy Adams, but that it sometimes calls him “John Q. Adams” and sometimes “John Quincy Adams.” If you want to standardize, you want to make the whole “uincy” field optional. You can do this by searching for the following regex:

`John Q(uincy)?.? Adams`

Note that you need the period too, or else it won’t match for John Q. Adams.

`.`

One last special character is the period, which matches any single character.

The most capacious regex of all is `.*`, which tells the parser to match “any character any number of times.” There are situations where this can be useful, particularly inside another regex.

`^`

Carats can be used to indicate you want your pattern to start at the beggining of a line. If typed after an opening square bracket, the caret negates the character class inside the brackets. Thus `f\[^i\]at` would match `feat` but not `fiat`.

`{}`

For most cases, `*`, `+`, or `?` will work to capture an expression. But if you want to specify a particular number of times, you can use angle brackets. So, in the email address example above, `{2,4}` is used at the end to indicate that we want to match the final *kind of pattern* indicated by the previous bracket 2-4 times (i.e., we want to look for at least 3-letter suffixes, such as `com` or `edu` at the end of addresses).

### Replacements
The syntax for replacing a regex will change from language to language, but the easiest substitution is to replace a regex by a string. Here we are using perl syntax, which gives the name of the operation (`s/` for "substitute", `m/` for “match”) separated by forward slashes (**Note**: If you are using RegEx 101 to complete this lab, you do not need to include `s\` or `m\` when using the site's "Substitution" function; it is implied). More recent languages or text editors may have a different syntax, but the important thing is that any substituting regex has two primary parts; the field to be matched, and its substitution.

### Escaping special characters
Sometimes, of course, you’ll actually want to search for a bracket, parenthesis, or other special character that appear in the text of your data.

To describe a literal bracket in a regex, you use the so-called “escape character”: the backslash, `\`. “Escaping” a character means putting a backslash in front of it, so that it takes a special meaning. To represent a literal period, for example, you’d have to specify the regex `\.`. The backslash is hardly ever used in normal writing, so it makes a safe choice for this: but you can always “escape” even the backslash itself, by prefacing it with another backslash: `\\`

### Group matches
In addition to escaping those special characters, regexes also allow you to create other special characters. The most powerful ones, and the ones best worth knowing, take their meaning from the context of the regular expression.

When you use parentheses in a regex, it doesn’t only create a group for matching: it also sets aside that group for future reference. Those can be accessed by escaping a digit from one to ten. That means that you can replace a string contextually.

If you wanted to replace every occurrence of “ba” in a text with “ab,” say, you could simply run the following substitution:

`s/ba/ab/`

Or, translated into the "Find"/"Replace" structure of RegEx 101:

Regular Expression: `ba` <br/>
Substitution: `ab`

But what if you actually want to swap any two letters?

`s/(b)(a)/\2\1/` does the same thing, but more generally. You could put anything into the parentheses. Here's that translated into RegEx 101 terms:

Regular Expression: `(b)(a)` <br/>
Substitution: `\2\1`

Say you wanted to reformat a list of names from Firstname Lastname format to Lastname, Firstname.

The regex `s/(.*) (.*)/\2, \1/` matches any characters, followed by a space, followed by any characters, and replaces them with the second group and the first group.

In RegEx 101:

Regular Expression: `(.*) (.*)`<br/>
Substitution: `\2, \1`

### Creating other special characters.
Other important special characters come from prefacing letters.

- `\n`: a “newline”
- `\t`: a tab

In addition, other special characters will match a whole range of letters. Usually, there would be a way to write these as a regular expression on their own: but it can be very helpful to have a more succinct version. Some of the most useful are:

- `\w`: Any word character. (The same as [A-Za-z]).
- `\W`: Any non-word character. (The same as [^A-Z-a-z])
- `\d`: Any numeric (digit) character.
- `\D`: Any non-numeric (digit) character.

(If you are working in non-English languages, there are unicode extensions that work off the special character `\p` (or `\P` to designate the inverse of a selection). `\p{L}` matches any unicode letter, for example. See the [unicode web site](http://www.unicode.org/reports/tr18/){:target="_blank"} for more on this.)
