# Data Literacy Field Notes & Terminal Log

**The scenario:** A climate-and-energy nonprofit wants to use this
country-level energy and emissions dataset to help decide where to direct
community-protection and climate-support efforts — but the file just
landed with zero documentation. Before anyone can trust a decision built
on top of it, you need to figure out what's actually in it — what each
column really holds, and anything that looks off. That's what this whole
file walks through: the real, everyday first pass any analyst runs on an
unfamiliar file, and the real answers you need before this data is safe
to act on.

Dataset: `../data/co2_emissions_2022.csv` (see `../data/SOURCE.md`). Each
section below describes what you're trying to find out — **figuring out
which command (and which flags) actually gets you there is part of what
this project tests**, so the exact command isn't given. Where a command
belongs, you'll see a `# TODO:` comment describing the goal instead of a
ready-to-run command; replace the comment with the real command you used.
Paste the **real output** you got underneath, then write your answer based
on what you actually saw, not what you'd expect. Work through this in
order; open the raw file before anything else.

Run all commands from the repo root — the top-level folder you land in
after cloning *your own* copy of this repo (`git clone ...` then `cd
your-repo-name`, see `README.md` Step 3; not this template) — or `cd` into
`data/` first and drop the `data/` prefix — your choice, just be
consistent.

**This one file is your whole record** — the commands you ran, their real
output, and your written answers, all together in the order you actually
did the work. There's no separate log file to keep in sync with this one;
whenever you write a command down anywhere in this file, use a fenced code
block tagged `bash`, like this:

````
```bash
git status
```
````

Three backticks, the word `bash`, your command, three backticks to close —
it renders with syntax highlighting and makes the command copy-pasteable.

## Setup log

Before jumping into the dataset, log the commands you actually ran to set
this repo up (see `README.md`) — `git init`/clone, creating your
`.gitignore`, your first commit. Add to this as you go, don't
reconstruct it from memory at the end.

```bash
# TODO: the commands you actually ran to set up this repo
git clone <repo>
cd <repo> 
```

## 1. First look at the raw file

Before trusting anything about this file's structure, you want a quick,
safe peek at it — not the whole 254-row file, just the **first 5 lines**,
enough to see the shape of it without scrolling past everything.

```bash
# TODO: a command that prints just the first 5 lines of the raw file
head -n 5 co2_emissions_2022.csv
```

**Output:**

country,iso_code,year,population,gdp,co2
Afghanistan,AFG,2022,40578847,53303471617,10.170
Africa,,2022,1445862695,,1459.114
Africa (GCP),,2022,,,1459.103
Albania,ALB,2022,2827614,36171005594,4.498

**What I notice:**
The first five lines includes the header which helps with understanding the following four lines and how they're organized/categorized. I also noticed Africa (GCP) doesn't have some info, such as iso_code, which makes sense since that encompasses the entire continent and isn't specific country data.

## 2. Column names

Next you want to see just the column names by themselves — one per line is
a lot easier to scan than one long comma-separated row.

```bash
# TODO: a command (or combination of commands) that prints just the header
# row, one column name per line
head -n 1 data/co2_emissions_2022.csv
```

**Output:**
_TODO_
country,iso_code,year,population,gdp,co2

## 3. Column-by-column data type table

For each column, you want to preview real values — **the first 6 values**
of just that one column — without scrolling through every field on every
row. Column numbers for reference: `country`=1, `iso_code`=2, `year`=3,
`population`=4, `gdp`=5, `co2`=6.

```bash
# TODO: a command that prints the first 6 values from a single column
# (repeat this for at least 5 of the 6 columns, swapping in each column's number)
cut -d ',' -f1 data/co2_emissions_2022.csv | head -n 6
cut -d ',' -f2 data/co2_emissions_2022.csv | head -n 6
cut -d ',' -f3 data/co2_emissions_2022.csv | head -n 6
cut -d ',' -f4 data/co2_emissions_2022.csv | head -n 6
cut -d ',' -f5 data/co2_emissions_2022.csv | head -n 6
cut -d ',' -f6 data/co2_emissions_2022.csv | head -n 6
```

Fill in the table from what you actually saw — not a guess from the column
name alone:

| Column | Inferred type | How I can tell |
| --- | --- | --- |
| country | str | letters |
| iso_code | str | letters |
| year | int | whole number |
| population | int | whole number |
| gdp | int | whole number |
| co2 | float | decimal |

**In your own words:** what's the actual difference between a list/array
and a table? (Not a definition you looked up — explain it the way you'd
explain it to a friend who's never coded. No command needed for this one,
just think about the table you just filled in above.)

The difference between a list/array and a table is how they're structured. A list or array have a set of individual values. Tables are sets of rows and columns, but lists are values in a sequence.

## 4. Structured or unstructured?

State whether this dataset is structured or unstructured, and why.

The dataset is structured because each column in the table has consistent data types. For example, `iso_code` is always a string of 3 letters, whereas `population` is always a whole number, making it an int consistently.

## 5. Before you trust this data

Your first look (see section 1) turned up a row with a suspiciously
**blank** `iso_code`. Before you build anything on this data, you want to
know exactly how many of the 254 rows share that blank — is it a one-off,
or a real pattern worth flagging before anyone draws conclusions from it?
You may need more than one command for this — piping (`|`) feeds one
command's output into the next as input.

```bash
# TODO: a command (or combination) that counts how many rows have a
# BLANK iso_code
cut -d ',' -f2 data/co2_emissions_2022.csv | grep -c '^$'
```

**Output:**
36

```bash
# TODO: the same idea, but for the gdp column
cut -d ',' -f5 data/co2_emissions_2022.csv | grep -c '^$'
```

**Output:**
89

List **at least 2** specific things you'd want to know about how this
dataset was collected, before trusting any conclusion drawn from it — ground
at least one in the counts you just found.

**My 2 concerns:**

1. Since the dataset includes more than just countries (like continents, countries groups by income, etc.), what determines how those are divided and categorized?
2. Why are some countries missing data in `co2`? 

## 6. Data-quality question for the source

Take the **most specific and checkable** of the two concerns above, and
phrase it as a real question you'd send to the data's source/maintainer. A
good test: could they actually answer it with a concrete yes/no or fact —
not "is this data good?"

How is each grouping available (income, continent, continent with some exclusions, etc.) determined?

## 7. Something you're actually curious about

Different question from #6 — that one was about checking the data's
trustworthiness. This one's about you: what's something you're genuinely
curious to explore using this data? Pick two specific countries you're
curious to compare, and look up their full rows.

```bash
# TODO: a command that finds a specific country's row by name (repeat for
# a second country of your choice)
grep -n "" data/co2_emissions_2022.csv
```

**Output:**

17:Asia (excl. China and India),,2022,,,7694.873
49:China,CHN,2022,1425179562,26966016991166,11711.808

**My question:** What causes China's CO2 emissions to be so high compared to other countries?

## 8. AI-literacy reflection

Name **2 concrete risks** of trusting an AI assistant's output about this
dataset (or any data question) without checking it yourself. Then state
**one specific personal rule** for when you'll double-check an AI-provided
fact before relying on it professionally — specific enough that you could
actually follow it, not "I'll be careful."

**Risks:**
1. AI saying something confidently and incorrectly about the data.
2. AI making up info about the data (i.e. about missing data points).

**My rule:** Verify all information that AI tells by double checking the data points it references and ensure it uses the same (or accurate) source(s).

## 9. Something that went wrong (and how you figured it out)

Somewhere in this project you're going to run a command that either throws
an error or gives you output that isn't what you expected — everyone hits
this at least once. Paste the actual command and what actually happened
(not a paraphrase), then explain what that told you and how it led to the
fix — not "I googled it and it worked."

```bash
# TODO: a command that errored, or gave you unexpected results
head -n 5 data/co2_emissions_data_analysis.csv
```

**What happened:**
head: data/co2_emissions_data_analysis.csv: No such file or directory

**What it told me and how I fixed it:** Since the directory didn't exist, I likely spelled it wrong. I realized I was putting in the wrong name of the csv. The CSV file is `co2_emmisions_2022.csv`, not `co2_emissions_data_analysis.csv`. 
