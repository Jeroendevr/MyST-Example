
When working in PowerBI there are multiple sub-elements that create a solid analytics structure.

1. General Design
2. Data Model Design
3. Report Design
4. Building Principles.


## General Design
Split the dataset with the underlying data model from your reports. Multiple reports can point to a single dataset. This makes sure that you maintain a single source of truth, instead that every report-maker creates their own version of the truth.

Add a 'Data' Report to your PowerBI workspace. In this report, you can jointly monitor data quality with your users. Here you can share if all data pipelines are correctly working. 
  

## Data Model Design
##### Version your data models. 
In this way you can safely develop and adjust the latest version and have an older version generate the dataset for all the reports that are used.

##### Use a dimensional star schema
Dimension tables. These describe attributes and characteristics of objects. A company can have an address, legal name, registration number
Fact tables. These are occurances of items like orders, transactions, hours
Utility tables. These are supportive tables that contain elements such as a date table and a data freshness table.

##### Measures
Store all measures in seperate folders seperate from the tables that are used to generate them.

When you want to use a metric in a report, create a measure for it, since you might want to make minor adjustments in the way it looks and behaves in a report. When you remove the table where a measure originaly came from, it will not be removed from your model, but will only throw an error in your reports. But you still have the scaffolding to adjust the input metric with the replacement value. Example: When you have a metric called 'Billable hours', you might want to add a daterange filter so the data is shown in a consistent manner. You create a new measure 'Billable Hours', and use that measure in all reports. 

Make sure that you setup the Fonts for each measure in the dataset, this prevents cumbersome adjustment in each report per individual visual.

##### Naming conventions
Adjectives should be place before the measure name. For example you have a measure called 'Hours'. You can seperate these hours among 'Billable Hours' and 'Non billable Hours'. 

Timing words should come first. So 'Billable Hours' that are in the past should be names 'Realised Billable Hours'

Be consistent with your naming conventions across your data model. When you use 1 measure as input in a DAX for another measure, you better understand what you are doing when all measure names are consistent.

Try to limit your naming conventions to max 3 words. Otherwise the countless combinations of measure scales too exponentionaly. For example 'Realised Billable Hours' has 3 other brothers. 1) 'Expected Billable Hours', 2) 'Realised Non Billable Hours', 3) 'Expected Non Billable Hours'. Adding a third adjective expands the number of combinations to at least 8. This number is too high for a mere mortal to comprehend.

##### Re-using measures
When you build measures. Use previously built measures. This way you create a consistent and scalable data model that is less likely to error and easier to work with. 

Do this: 'Billable Hours' = 'Realised Billable hours' + 'Expected Billable Hours'. Instead of rebuilding the two measure that were used in this example. When you change one of the measures in the future, you have to change it at least two times. 

Especially when your data model becomes more complex and measures use other measures that use other measures. You keep things comprehendable with this setup when complexity grows.

##### DAX
Try to use as many tabs as possible, splitting your calculations up. It improves readibility and de-bugging.

You can use comments in DAX using //. Use it when you build more complex calculations. Both for later self and other people working with your DAX and data model.

##### Data transformations
Don't use PowerBI for data transformations. PowerBI has no central repository where you can effectively collaborate on the data model. Use [[dbt Cloud]] instead.

When you have a metric called 'Hours' and you want to determine which of those hours are 'Billable Hours' do that in dbt Cloud. This makes sure that we have a single truth called [[master data]] where powerbi pulls its data from.

##### Content
Check out [Guy in a Cube](https://www.youtube.com/c/GuyinaCube) for in depth tips and tricks on data model design.


## Report Design
##### Page clusters
1) Analytics: You answer specific questions that are key to the report users

2) Hygiene: The dataset should be clean and consistent. Use dedicated pages within the report to focus on the data hygiene. With visuals that support comparing multiple input values and see if they add up or totaling zero etc.

3) Input data: Your report contains multiple data sources that are used. As users find patterns are peculiarities in their findings, sometimes you want to deep dive into the raw data that is at the core of the entire dataset. Allow users to find the individual records to the smallest level.

4) Definitions: Describe all measures, on what underlying logic they are generated.

##### Same template
Consistency and familiarity creates a better User Experience.

Use the same positioning of filters across all pages of a report and preferably across all reports.

Position individual filters on exactly the same location, so users are not have to look for filters in each page.

Apply the same coloring, font sizes, positioning of logos on all your reports.

##### Same filters
Across all Analytics and Hygiene pages, use the same filters. This implies that when you have 6 pages that answers a specific question, a specific measure should show you the same exact number, independent of the page you are looking at.
Use the same filters-dropdowns on all analytics and hygiene pages. In this way, for the user, it feels like they are using the same environment to analyse and look at a set dataset.
Sync all analytics filters across all analytics and hygiene pages. So when you select a specific dimension value, then this filter is applied to all pages.

##### Report & Page Numbering
Use a distinct number for your each report and pages. This way you can effectively communicate between users and engineers.

Feel free to move around numbers. Numbers are allowed to change.

Use the same page number and name both in the tabs and in the left corner

##### Graphs
Be cautious in using too many visuals, especially complex visuals. Graphs often are seen by users as sexy, but they usually have limited value when it comes to communicating a message and digging deeper.

When you want tot use graphs, try to keep them as clean and simple as possible. Every additional color, measure makes the graph harder to read and graphs take up precious page real-estate.

##### Scorecards
Use 3-6 scorecards per page, that aggregates a certain measure. This allows users to quickly make sure they applied the right slicer. Also comparing pages, these scorecards should show the same values. This setup allows users to get the feeling the really understand the data they are juggling with.

Try to use a consistent order, from left to right, where possible, when showing similar scorecards on multiple pages.
When a scorecard is too small. Abbreviate words in a sensical way. Scorecards with too long measure-names where you can only ready half, diminishes the user's understanding of the page.

##### Colored tables/matrix
Using custom rules to adjust the background colors of a table or matrix are a very effective way to allow the user to focus on those measures that are relevant. Looking at a table with 20 columns and 100 rows with percentages without colors is very draining and often too cumbersome for an user to even consider.

##### Content
Check out more report design videos on [How to Power BI](https://www.youtube.com/c/HowtoPowerBI/featured) hosted by Bas Dohmen.


## Building Principles
When you adjust a measure or report visual, make sure you properly spot-check your adjustment, comparing it to similar measures on the same page and other pages in PowerBi. Apply common sense when you change something and consider its points of failure.

When you work on a report and you want to answer a user's question, browse through the data, and interact with the report as you were the user and ask yourself, if I were the user does this feel intuitive and easy to use? 

When you make a major adjustment to a page, and you and/or the user are not yet convinced this is an improvement, create a seperate page with your abbreviation added at the end. For example: '604 
Billable Hours' becomes '604 Billable Hours (PBO)'

When you create a new page/report. Make sure it is paying tribute to the design principles described here. 


