# MarSpatAuto
Automating marine spatial date acquisition &amp; analysis


# Automating (marine) spatiotemporal data processing, acquisition and analysis
Simon Dedman, 2020-11-12, simondedman@gmail.com www.simondedman.com 

# Background
Taggers & trackers of sharks and other large marine species typically collect the same type of data, and then one person spends countless days researching which explanatory variables / correlates they should try to acquire, tries to acquire them, acquires some, possibly researches how best to format them, formats some, researches which test to use to get the result they’re interested in, uses probably one of them, occasionally the best one, researches what the results mean, and then spends days plotting and replotting figures and tables, and poring over them.

This solitary drudge work perpetuates despite our living in The Future, surrounded by powerful computers and mostly using the same two free programming languages which host innumerable freely-shared tests. Arguably this endemic tedious yeomanlike wheel-reinventing is due to the structure of science and academia, resulting in its being inherently brutally anti-collaborative and therefore highly inefficient when considered as a single sector.

I propose that the majority of the ostensibly-highly-technical work that often comprises the bulk of the time spent on science, could be automated down to requiring only the barest user input, for any analytical technique that has been coded and shared. This would free up humans to do things that humans want to do (fieldwork, research) and are better at (interpreting findings into the wider contexts of ecology, policy, management, etc.). 

# What do we have?
Tag data from large marine species typically have latitude, longitude, and datetime (typically daily). They maybe have (ARGOS) satellite strength (codes) or similar spatial error metrics, fish size, and other sensor readings like depth, internal and external temperature, light level, DO2. They might have additional metadata parameters like the ID of different individuals in the case of data contain multiple tracks, and similar metadata grouping columns like sex, stock, etc.

# Which correlates?
Some are obvious: temperature, ocean depth. Most others require increasing levels of experience / background in the field (of marine spatio-temporal analysis) to know about. This is a barrier to entry. 
Correlate research & gathering is typically a substantial part of a project, and is a drudge.
Too few correlates can result in low explanatory power or, worse, acceptable explanatory power and a conclusion that misses key drivers of the studied system.
Simple spatiotemporal projects are a staple of early career science work but a failure to complete exhaustive assessment of plausibly pertinent variables is chronic.

So: deciding which correlates you’re even interested in is a problem.
But it’s a solvable problem: one thorough literature review would probably find 99% of variables that folks have used. My hope is that community members will simply share their variables and code.

# From where?
Erddap, rerddap, rextracto, libraries of databases, and extraction tools, already exist.
But also, my voluminous bookmarks of data sources. NASA, Planet, local agencies (Florida mangroves), NGOs (Allen coral atlas), Rebecca Degagne’s team.
There are many large data holders, some of whom are trying to index all marine spatial data in one place (ERDDAP, Rebecca). [Warning: ensure this project isn’t Reinventing the wheel]
We’re not aiming to replace or compete with these database libraries nor their extractions tools, where they exist, rather we’re looking to leverage them into an overarching system which removes the work of sourcing the appropriate correlates for your XY(Z)T data, given that there can only be one publicly-available highest-resolution source for any XYZT point.

# What format?
Because the ‘Big Ones’ are obvious (temp: °C; salinity: ppm) it’s easy to stride from acquisition to analysis without thinking about processing. How do you account for date? Yearday? So this variable  shrinks to 1/365th its size on New Year’s Day? That’s some hangover. Month? A way of dividing a year by lunar cycles using a system that isn’t exactly tied to lunar cycles? And for the lunar signal - % of full? Cycle position in radians?
Again, these are researchable answers. But, for every one of potentially tens of variables. That you already researched and took ages acquiring.
Very likely, we as a community can agree on a best format and that’ll be that. If there are genuine alternatives, fine, we can provide both formats, document that, and allow the user to choose the alternative(s) if they so wish.

# What tests?
So you provided your lat lon & datetime and now you have a whole slew of extra columns of data. Hoorah! Now what? Literature review for “best” technique to answer a specific question that was arbitrarily conceived in the original project hypothesis that led to the data being gathered. Technique chosen is likely a compromise of commonality of use, ease of acquisition, ease of understanding, ease of use, and ease of understanding of results. A single-technique analysis approach is likely. Two occasionally. >3 rare.
The aim, therefore, is to analyse the data using the best version of every applicable (s/t) analysis technique.
Inclusive of pre-testing for S/T autocorrelation of original data & autocorrelation of new correlates.

# What do the results mean?
So you ran all these tests and R spat out a whole slew of opaque values and coefficients, across hundreds of screen-height scrolls. Hoorah? Now what? Literature review for the meaning of each of these. Presume that information on how to interpret all elements of a test result exists (they don’t always). Presume that available information warns about risks from certain data types and/or formats (they don’t usually). Re-run the test but this time assign the output to an object so you can use it. Spend days formatting plots and tables so you can display and share said results.
ALL of this is formulaic and can be codified. It’s a time-well that disproportionately swallows earlier career researchers, until they level up their background knowledge and (gg)plotting skills.

Instead:

Contextualised meaning of results, using simple text code in R (if P<0.2 then “this result is significant”), plain English interpretation, with references and quoted text blocks of key bits from those papers as appropriate.
All individual results plotted and saved as images into folders with appropriate names, and accompanying text files for suggested captions. R Markdown (& pdf, html) reports created for each test.

And even then there’s drudge that can be automated. It’s great that we can produce hundreds of plots with a few lines of code. But you now have to analyse and common-sense-interpret hundreds of plots, scribble notes for each, decide which are important and/or interesting, consider their interactions, coalesce this into a physically/biologically/ecologically-contextualised story. Again, much of this is formulaic, even if it may not feel that way initially.
Firstly, simple plot analysis. If that correlate is contributing nearly zero explanatory power, ignore it. Easy enough right? Tell me you’ve never looked at those plots. Tell me you haven’t thought “that’s quite interesting” even though you know the caveat is that this correlate explains 0.001% of the variance. You can’t get those brain cycles back.

Harder stuff that’s still easy: is it a linear relationship? Curvilinear? Which way is it going? “More of X results in less of Y”. “Y has a domed relationship with X which peaks when X is 4”. Are there thresholds? “Y is notably higher when X > 2.79”.
Take those, order them by variable importance. Couch paragraphs in those terms: “Salinity explains 7% of the variance so its relationship with bull shark abundance is of relatively low but not insignificant value.” Etc.
Secondary interpretations can be similarly codified (community input/legwork will be key here); temperature and depth have a known relationship so if both are present then a default paragraph can be included, followed by a dynamic text chunk which relates to the interaction strength in the results, the importance of each to the variance, etc.

Tertiary (ecological / ecosystemic) results can be codified, given more work. “The data are predominantly from these depths and distances from shore, suggesting this is a coastal pelagic species. Known important drivers for this ecosystem group are A B and C, which are all found to be important in this analysis”. [This element of the results could be community collaborative, with results submittable to a shared database that could be queried for trends, feeding back to the interpretations for others. Generate results interactions pairplot matrix for all correlates, to populate with default text blocks & dynamic text code].

Overall results for all tests and pre-checks synthesised into a single report (markdown, html, pdf) with tables, figures, and text.

# How will the package be organised?
Modular, component R scripts formatted to accept the standardised input data.

Order:

1. Check input data – are positions all marine (if this is marine only), datetime in order, no duplicates, (anything else)? Plot basic stuff. Save in standardised folder structure.

2. Test input data for autocorrelation, other tests? Save report in folder.

3. Computer system check: all packages installed & loaded, get system details to provide time estimates (later). Additional (numbered) report.

4. Correlate acquisition. Collectively agree defaults – most but maybe not all? And which variants e.g. satellite ChlA: daily, 3day, 8day, month, etc. User options to change these. Ability to ingest user’s own correlates where not universally available. Save output df and make table of variables used with resolution (& other data details), sources & references (user-ingested data to be accompanied with these details in text file, csv, bibtex, etc).

5. Correlate formatting (do as part of above?)

6. Run tests. User options of which to run, default all? Likely default most. Pre-check of estimated time per-test & total. Option to restart. Save results (data, plots, etc.?) to per-test subfolders. Script format: probably 1 control script which calls individual tests scripts and final report script. Tests scripts run the tests (duh) and also do the plotting, reporting, file saving. Report script stitches together individual subfolder reports into sections, including initial data plots & status, processing done, autocorrelation results, correlates used table.

7. Free on Github & CRAN.

# How do we start?
Github project. Also some kind of community location, email list?
List of tests. And existing packages. And code experts for those packages who’ll be prepared to assist in writing the automation script.

# List Of Tests
Habitat comparison: if you have a vector of lat lon datetimes, and get the accompanying environmental variables, you can compare the habitat subset against a larger habitat subset (e.g. our study area vs whole known species range) or total global habitat (i.e. ignoring the species data).

Electivity: follows from above

Core use area, minimum 50% 75% 90% kernel use density polygons, including coastline removal.

Kmeans XYT behaviour bins, resident vs migration

Importance & relationship of environmental predictors to spatial abundance, gbm.auto etc

Outcomes supplementary material document idea

Idea for a standard-format SM doc which contains the bibtex of the main manuscript, and an unlimited number of single line text fields for individual outcomes/facts from the paper, i.e. what the paper contributes in terms of new content/knowledge/facts, in plain English. E.g.:
    • smalltooth sawfish prefer water temperatures between 23.3 and 27.4°C
    • stress hormone is moderately positively correlated to lactate in tiger sharks
    • female cownose rays reach sexual maturity at 5.3 years old (4.6 – 5.9 1SD)
“There is a set of standard-tags (aka fields) existing, which can be interpreted by BibTeX or third-party tools. Those which are unknown are ignored by BibTeX, thus can be used to store additional information without interfering with the final outcome of a document. ” http://www.bibtex.org/Format/ 
Could use the note field https://www.bibtex.com/format/ multiple times allowed. Could also add SM links here?

# Ok so what do *I* do?
Go to issues, think of an explanatory variable you use. Is there an issue for that? No? Create one. Go one better and find the highest res publically availavle dataset for that. If nothing else, create the issue.
