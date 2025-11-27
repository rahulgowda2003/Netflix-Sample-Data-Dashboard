# Netflix Sample Data Dashboard


## Problem Statement

This dashboard provides an analytical overview of Netflix’s sample content from 2010-2022.

It helps stakeholders understand:
- The size of Netflix's content library
- Distribution of TV shows vs movies
- Release trends over time
- Global content availability and consumption
- Genre-based filtering
- Viewer preferences by certificate rating
- Runtime insights for movies

The dashboard can support content strategy, regional expansion decisions, and catalog optimization.


### Steps followed 

- Step 1 : Load the data into Power BI Desktop, the file was in csv format.
- Step 2 : Opened power query editor and in view tab, under Data preview section, check "column distribution", "column quality" and "column profile" options.
- Step 3 : By default, column profile will be opened only for 1000 rows, so you will need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors and empty values were present except in columns named "Rating", "Release Date", "Country",
           "Cast" and "Director".
- Step 5 : For calculating null values, replaced the null values with the mode of the same column(for the numerical values present having <1% null values and
           categorical column with <1% null values were removed) and for the other categorical values with >5% null values, filled the null values as "Unknown".
- step 6 : New column named "Release Year" made to extract the year from "Release Date" column, the null values present in the "Release Year" was filled with
           mode.
  
           a) DAX for Release Year = YEAR(Netflix[Release_Date])
- Step 7 : In the report view, added Netflix's logo and name tag.
- Step 8 : Visual filters (Slicers) were added for two fields named "Release Date" and "Genre".
- step 9 : Five measures careated in the new model named "Measure's Table" and one in Netflix's table. Measure's Table contains Avg movie runtime, count of cast,
           movies, num of titles and TV shows, where as in the Netflix's table contains Runtime measure.
  
           a) DAX for Avg movie runtime = CALCULATE(AVERAGE(Netflix[Runtime (Minutes)]),
                                                            Netflix[Category] = "Movie")
  
           b) DAX for Count of cast = DISTINCTCOUNT(Netflix[Cast])
  
           c) DAX for Movies = COUNTROWS(FILTER(Netflix,
                                                Netflix[Category] = "Movie"))
  
           d) DAX for Num of titles = COUNT(Netflix[Title])
  
           e) DAX for TV Shows = COUNTROWS(FILTER(Netflix,
                                                  Netflix[Category] = "TV Show"))
  
           f) DAX for Runtime (Minutes) =  VAR txt0 = LOWER( TRIM( Netflix[Duration] ) )
                                           VAR txt1 = SUBSTITUTE( SUBSTITUTE( SUBSTITUTE( txt0, "mins", "" ), "min", "" ), "minutes", "" )
                                           VAR txt2 = SUBSTITUTE( SUBSTITUTE( txt1, "seasons", "" ), "season", "" )
                                           VAR txt3 = TRIM( txt2 )
                                           VAR pos = FIND( " ", txt3, 1, 0 )          // position of first space (0 if none)
                                           VAR numText = IF( pos > 0, LEFT( txt3, pos - 1 ), txt3 )
                                           VAR numValue = IFERROR( VALUE( numText ), BLANK() )
                                           RETURN
                                           numValue
  
- Step 10 : Five card visuals were added to the canvas/dashboard, representing "count of cast", "TV Shows", "Movies", "Total Content" and "Average Movies Runtime".
            Using visual level filter from the filters pane, basic filtering was used & null values were unselected for consideration into average calculation.
- Step 11 : Filled map was inserted to showcase the content consumed by the countries around the world. 
- Step 12 : Line chart was added to present the TV shows and movies released by year.
- step 13 : Stack bar chart, to get the insights for the most content consumed by countries around the world.
- step 14 : Stack column chart to show the TV rating for the content present in the sample data of Netflix.


  # Report Snapshot (Power BI DESKTOP)

 
![Dashboard_upload](https://github.com/rahulgowda2003/Netflix-Sample-Data-Dashboard/blob/main/Netflix%20Dashboard%20Screenshot.png)

# Insights

a) KPIs
- Count of Cast : 6828
- TV Shows : 2408
- Movies : 5373
- Total Content : 7781
- Average Movie Runtime : 99 minutes
  
These metrics show Netflix currently hosts a large catalog with a higher share of movies than TV shows.

b) Slicers
- Genre : Dropdown (All / Individual Genres)
- Release_Date : Dropdown (Year-based selection)
  
These slicers enable dynamic exploration of content trends.

c) Visual Descriptions

1] Line Chart - TV Shows and Movies by Release Year

Shows content release trends from 2010 to 2022.

Observed values:
- 2010 - TV Shows: 1, Movies: 1
- 2015 - TV Shows: 18, Movies: 6
- 2020 - TV Shows: 1498, Movies: 430
- 2021 - TV Shows: 69, Movies: 19
- 2022 - Further decline visible
  
Massive spike between 2017–2020, followed by a noticeable drop, likely due to production slowdowns.

2] Map Visual – Global Content Distribution

A world heatmap highlighting countries with higher Netflix content availability/consumption.

Darkest areas:
- North America
- Europe
- South Asia
- Parts of South America
  
This reflects Netflix’s strongest markets.

3] Bar Chart – Content Consumed by Countries

Countries:
- United States : 2552
- India : 923
- Unknown : 506
- United Kingdom : 397
- Japan : 225
- South Korea : 183
- Canada : 177
- Spain : 134
- France : 115
  
The US remains the dominant market. "Unknown" likely indicates missing metadata.

4] Bar Chart – Most Watched by Certificates

- TV-MA : 2865
- TV-14 : 1931
- TV-PG : 805
- R : 665
- PG-13 : 386
- TV-Y : 280
- TV-Y7 : 271
- PG : 247
- TV-G : 194
- NR : 84G39
- TV-Y7-FV : 6
- UR : 5
- NC-17 : 5
- Classic Movies : 1

TV-MA and TV-14 make up the majority of watched content.

d) Insights Based on Dashboard

1] Content size

- Netflix has 7,781 total titles
- Movies outnumber TV shows nearly 2:1

2] Runtime insight

- Average movie runtime ≈ 99 minutes

3] Country consumption

- United States leads by a large margin
- India is the second-largest market

4] Certification preference

- Mature-rated content (TV-MA) dominates, indicating adult audience preference

5] Release trends

- Massive spike in content releases between 2016–2020
- Slight decline post-2020 (likely due to pandemic impacts)


e) Snapshot Description

The dashboard uses:

- Dark Netflix-style theme
- Bold red borders
- Clear layout: KPIs → Filters → Visuals
- Mix of map, bar charts, line chart, and KPIs
