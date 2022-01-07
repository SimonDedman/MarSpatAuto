# MarSpatAuto
Automating marine spatial date acquisition &amp; analysis


# Automating (marine) spatiotemporal data processing, acquisition and analysis
Simon Dedman, 2020-11-12, simondedman@gmail.com www.simondedman.com 

# Background
Taggers & trackers of sharks and other large marine species typically collect the same type of data, and then one person spends countless days researching which explanatory variables / correlates they should try to acquire, tries to acquire them, acquires some, possibly researches how best to format them, formats some, researches which test to use to get the result they’re interested in, uses probably one of them, occasionally the best one, researches what the results mean, and then spends days plotting and replotting figures and tables, and poring over them.

This solitary drudge work perpetuates despite our living in The Future, surrounded by powerful computers and mostly using the same two free programming languages which host innumerable freely-shared tests. Arguably this endemic tedious yeomanlike wheel-reinventing is due to the structure of science and academia, resulting in its being inherently brutally anti-collaborative and therefore highly inefficient when considered as a single sector.

I propose that the majority of the ostensibly-highly-technical work that often comprises the bulk of the time spent on science, could be automated down to requiring only the barest user input, for any analytical technique that has been coded and shared. This would free up humans to do things that humans want to do (fieldwork, research) and are better at (interpreting findings into the wider contexts of ecology, policy, management, etc.).

Related article, concept contextualised within the wider future of humanity as relates to software and AI: https://medium.com/@SimonDedman/ai-and-the-future-of-marine-science-68a53dcd313d

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

0. set overall theme for all plots & reports which can be changed. E.g. per journal. Like CSL files. Colour-blind friendly. Viridis2.

1. Check input data – are positions all marine (if this is marine only), datetime in order, no duplicates, (anything else)? Plot basic stuff. Save in standardised folder structure. Ingest samples, clean, report.

2. Test input data for autocorrelation, other tests? Outliers, residual analysis, random forest imputation, etc. Save report in folder.

3. Computer system check: all packages installed & loaded, get system details to provide time estimates (later). Additional (numbered) report.

4. Correlate acquisition. Collectively agree defaults – most but maybe not all? And which variants e.g. satellite ChlA: daily, 3day, 8day, month, etc. User options to change these. Ability to ingest user’s own correlates where not universally available. Save output df and make table of variables used with resolution (& other data details), sources & references (user-ingested data to be accompanied with these details in text file, csv, bibtex, etc).

5. Correlate formatting (do as part of above?)
 
6. acquisition: embarassingly parallel: all rows of XYZT, for all variables.
acq.SST.source()
have people dump their scripts of functions into subfolders on github by var e.g. “acq.SST”. Regardless of how messy they are.
Ideally have a compressed boolean/logical 4D raster for the data they have (i.e. 4D space of data provision they occupy). Get text info from the data source, then convert.
For saving outputs: Add an index column to the samples df and save acquired data with just have an index column, i.e. 1c * Nr instead of 4c * Nr. Stitching scripts later can then join by Index only. Save as high compression R files.

7. Run tests. User options of which to run, default all? Likely default most. Function to deselect tests if it's mathematically unreasonable/illegel to run them on these data for whatever reason. Not sure what the reason would be given the point is the data are all tracking? Or any XYZT i.e. could be acoustic. Pre-check of estimated time per-test & total. Option to restart. Save results (data, plots, etc.?) to per-test subfolders. Script format: probably 1 control script which calls individual tests scripts and final report script. Tests scripts run the tests (duh) and also do the plotting, reporting, file saving. Report script stitches together individual subfolder reports into sections, including initial data plots & status, processing done, autocorrelation results, correlates used table. See https://github.com/tidymodels/tidymodels & https://www.tidymodels.org/ & https://www.tidymodels.org/learn/ and build around that format.
Use tidymodels where possible: individual scripts to analyse, generate results including errors, model evaluation, plots, save model objects for others to plot differently. Scrape acquisitions folders for available variables. Specify groups & XYZT subsets here.

7.5 Results meta-analysis (meta-results?): Do this here as part of each anl.SST.source() script, OR separately after, in case cross-variable insights allow increased reduction of results number? Maybe both: within-var reductions here, then

8. Across-var results meta-analysis & reduction, insights generation.
Synthesising Huge Results Stack: 
If analysing the same types of data, the results outputs will have the same biological meaning.
Those numerical results (e.g. linearity index = 0.8) can thus have simple text lines (e.g. "this is a straight path indicative of migration").
Expanding this, whole suites of results can be summarised e.g. "the path is STRAIGHT and LONG. The home range is LARGE; compared to the JUVENILE stage, the ADULT home range is LARGER. Etc".
Expanding THIS, multiple groups (e.g. adult/juvenile above) can have comparison summaries. "LEMON SHARKS have smaller home ranges than BULL SHARKS".
This can all be collated into a report.
Which bits are the most important? Differences I suppose. So it could highlight differences by sorting outcomes by differential.
AND THEN, potentially there could be a way to evaluate which results components are most informative to specific conclusions. I'm thinking PCA here maybe.
Results shape evaluation. If you have line plots of variables' relationships, those can probably be decoded with some relatively simple algorithmic rules. Is the relationship positive/negative, is it strong, is it linear, curvilinear, threshold, threshold where. Convert all that to numbers and again give the plain text meaning.
If you have lots of results which mean the same thing (plots metrics are similar), that should be easy to show e.g. with K-means clustering. Then you could sort & prioritise the 'best' of those similar results.

9. Free on Github & CRAN.

# How do we start?
Github project. Also some kind of community location, email list?
Acquisition: have people dump their scripts of functions into subfolders on github by var e.g. “acq.SST”. Regardless of how messy they are.
Ideally have a compressed boolean/logical 4D raster for the data they have (i.e. 4D space of data provision they occupy). Get text info from the data source, then convert. Script to automatically A-union-B 4D join all 4D data presence rasters per variable subfolder.
Tests: List of tests. And existing packages. And code experts for those packages who’ll be prepared to assist in writing the automation script.
Per acquisition: have people dump their scripts there. Might just be few-line functions. But should confirm to report output formatting.

# List Of Tests
Habitat comparison: if you have a vector of lat lon datetimes, and get the accompanying environmental variables, you can compare the habitat subset against a larger habitat subset (e.g. our study area vs whole known species range) or total global habitat (i.e. ignoring the species data).

Electivity: follows from above

Core use area, minimum 50% 75% 90% kernel use density polygons, including coastline removal.

Kmeans XYT behaviour bins, resident vs migration

Importance & relationship of environmental predictors to spatial abundance, gbm.auto etc

# Ok so what do *I* do?
Go to issues, think of an explanatory variable you use. Is there an issue for that? No? Create one. Go one better and find the highest res publically available dataset for that. If nothing else, create the issue. Or create an issue to chat about any element of this. Cheers!
