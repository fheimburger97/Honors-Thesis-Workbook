Final Project: The Socioeconomic and Food Reatil Landscape of San
Francisco’s Mission District
================

By: Fischer Heimburger (@fheimburger97) & Caroline Mahdavi (@cmahdavi)

# Introduction

The Mission District (known as “This Mission”) in San Francisco known
for it’s widening economic inequity, relatively high ethnic
diversity–including being a local hub for Latinx culture and heritage,
and vibrant food scene. This research seeks to first cultivate an
understanding of the socio-economic landscape of the Mission District,
and then initiate research on how this landscape is reflected in the
distribution of food retailers.

Economic inequity is a major challenge facing the Mission District
today. In 2020, it was found that “the highest and lowest income
brackets compose almost 40% of all Mission households” ([Mission Action
Plan
2020](https://default.sfplanning.org/Citywide/Mission2020/MAP2020_Status_Report_2018.pdf).
This demonstrates the increasing income gap experienced in the Mission
District. In addition, the economic landscape of the Mission District is
highly influenced by gentrification–the process by which the migration
of high-income residents to a place displaces low-income, often
marginalized, residents ([Chapple and Thomas
2021](https://www.urbandisplacement.org/about/what-are-gentrification-and-displacement/)).
San Francisco was recently found to be the most intensely gentrified
city in America ([Richardson, Mitchell, and Edlebi
2020](https://ncrc.org/gentrification20/)) and the Mission District, one
of the neighborhoods with the most advanced levels of gentrification
([Chapple and Thomas
2021](https://www.urbandisplacement.org/about/what-are-gentrification-and-displacement/)).
We hope to understand this unique and stark economic landscape by
mapping out median household incomes by census tract within the Mission
District. Our research on this is influenced by data and figures from
the [Urban Displacement Project](https://www.urbandisplacement.org/).
The Urban Displacement Project traces gentrification throughout the San
Francisco Bay Area. As a part of their studies, they gather data on
median income levels within the Mission District and map out their
findings. We hope, in part, to recreate aspects of their figures with
updated census data.

While much of the Bay Area is growing more racially segregated
([Menendian, Gambhir and Gailes
2021](https://belonging.berkeley.edu/roots-structural-racism)), The
Mission is unique for its relatively high ethnic diversity ([Hom
2021](https://missionlocal.org/2021/07/the-mission-isnt-as-racially-segregated-as-the-bay-does-that-point-to-gentrification)).
While overall in 2019 the Mission District was 38.7% Latinx, 36.4%
White, and 13.7% Asian ([City Data
2021](https://www.city-data.com/neighborhood/Mission-District-San-Francisco-CA.html));
the demographic makeup of race varies depending on locale ([Hom
2021](https://missionlocal.org/2021/07/the-mission-isnt-as-racially-segregated-as-the-bay-does-that-point-to-gentrification)).
Additionally, recent years have shown dynamic shifts in demographics as
the 2020 Census revealed a 14.4% decline in Latinx residents within the
Mission District and a 34.8% increase in Asian residents ([Horowitz and
Jarret
2021](https://missionlocal.org/2021/09/census-2020-as-san-francisco-grew-the-ethnic-makeup-of-its-neighborhoods-changed-heres-how)).
The [Othering & Belonging
Institute](https://belonging.gis-cdn.net/us_segregation_map/?year=2020)
researches levels of segregation in the San Francisco Bay Area. As part
of their research, they have created maps of the Mission District that
display levels of segregation and racial diversity. We seek to create
similar maps that display racial majorities by census tract to further
understand the demographic landscape of The Mission. We then hope to
understand how these socio-economic landscapes interact the landscape of
food retailers in the Mission District.

Food systems are complex, interconnected bio-physical and socio-economic
webs that are influenced by environmental, social, political, and
economic systems, institutions, and actors ([Ericksen
2008](https://doi.org/10.1016/j.gloenvcha.2007.09.002)). For many living
in cities, like those within the Mission District, relationships with
food systems revolve around food retailers—including supermarkets,
grocery stores, corner markets, and convenience stores—that help connect
food producers with food consumers ([Trivette
2019](https://link.springer.com/article/10.1007/s10460-018-9885-1)).
Using data from the [City of San
Francisco](https://datasf.org/opendata/), we hope to map out the current
distribution of food retailers in the Mission District. Then we seek to
understand how this distribution may be interconnected with class and
race.

Our research is organized as follows. First, we map out income levels by
census tract in the Mission District. Second, we map out racial
majorities by census tract in The Mission. We then create a demographic
table that organizes the socio-economic landscape of the district. In
the fourth section we map out the distribution of food retailers within
the Mission District. Lastly, we overlay the socio-economic maps with
the food retailer map.

#### Data note: We used the following libraries to analyze our data. Additionally, please run `install.packages("tidycensus")` in the console window.

Google API Key – need to upload key
\#`{r} register_google(key = "", write = TRUE) #`

``` r
retail_data <- read_csv("Food Retail Final List (Edit 3_30).csv") %>%
  select(!"Timestamp")
```

    ## New names:
    ## * `` -> ...46

    ## Rows: 97 Columns: 49
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (35): Timestamp, Name of Food Retailer, Address, Date Assessed, Type of ...
    ## dbl (12): Median Price of a Dozen Eggs, Median Price of a Loaf of Bread, Mil...
    ## lgl  (1): ...46
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
retail_data$coord <- paste(retail_data$lon, retail_data$lat) 
retail_data
```

    ## # A tibble: 97 × 49
    ##    `Name of Food Reta…` Address `Date Assessed` `Type of Store` `What type of …`
    ##    <chr>                <chr>   <chr>           <chr>           <chr>           
    ##  1 Mission Foodhall     3100 1… 1/26/2022       Specialty Food… Foodhall        
    ##  2 Fred’s Liquors & De… 200 Va… 1/26/2022       Grocery Store   <NA>            
    ##  3 E And M Market       399 Va… 1/26/2022       Convenience St… <NA>            
    ##  4 K & H Liquor         501 Va… 1/26/2022       Convenience St… <NA>            
    ##  5 Valencia Whole Foods 999 Va… 1/26/2022       Grocery Store   <NA>            
    ##  6 Decamere Market      1001 V… 1/26/2022       Convenience St… <NA>            
    ##  7 Indian Spices and G… 3265 2… 1/26/2022       Specialty Food… Ethnic Store    
    ##  8 Valencia Farmer’s M… 1299 V… 1/26/2022       Grocery Store   <NA>            
    ##  9 Valencia Grocery     1300 V… 1/26/2022       Convenience St… <NA>            
    ## 10 Mr. Liquor           1200 V… 1/26/2022       Convenience St… <NA>            
    ## # … with 87 more rows, and 44 more variables: `EBT Accepted?` <chr>,
    ## #   `Number of Locations (chain?)` <dbl>, `Median Price of a Dozen Eggs` <dbl>,
    ## #   `Median Price of a Loaf of Bread` <dbl>,
    ## #   `Median Price of a Gallon of Milk` <chr>, `Milk Standardized_Gallon` <dbl>,
    ## #   `Median Price of Oranges` <chr>, `Orange Standardized_lbs` <dbl>,
    ## #   `Median Price of Organic Oranges` <chr>,
    ## #   `Organic Oranges Standardized_lbs` <dbl>, …

## I Tract Income Typology

#### Table 1.1: Downloading San Francisco’s Geopackage

First, we downloaded the [geopackage for San
Francisco](https://github.com/urban-displacement/displacement-typologies/tree/main/data/downloads_for_public).
In the following chunk, we load the geopackage using `read_sf` and
`filter` for census tracts in the Mission District. We `select` to show
“GEOID” and “geom” which will help create our map.

``` r
gfile <- read_sf("sanfrancisco.gpkg") %>%
  select(GEOID, geom) %>%
  filter(GEOID == "6075020200" | GEOID == "6075020100" | GEOID == "6075020800" | GEOID == "6075020700" | GEOID == "6075022902" | GEOID == "6075020900" | GEOID == "6075017700" | GEOID == "6075022901" | GEOID == "6075022803" | GEOID == "6075022903" | GEOID == "6075022801" | GEOID == "6075021000" | GEOID == "6075022802")
```

#### Table 1.2: Downloading San Francisco’s Demographics

We then use `read.csv` to load typology data from the [Urban
Displacement Project
github](https://github.com/urban-displacement/displacement-typologies/tree/main/data/outputs/typologies).
The definitions for variable names can be found
[here](https://github.com/urban-displacement/displacement-typologies/blob/main/data/outputs/typologies/typologies_codebook.md).

``` r
demographics <- read.csv("https://raw.githubusercontent.com/urban-displacement/displacement-typologies/main/data/outputs/typologies/SanFrancisco_typology_output.csv")
```

#### Table 1.3: Median Household Income Table

First, we create the **medianincome** table which shows “GEOID” and
“hinc_18”; “hinc_18” is the median household income in the past 12
months (in 2018 inflation-adjusted dollars) in 2018. Second, with
`left_join`, we join the newly created **medianincome** table and the
initial **gfile** table to create our **incomejoin** table.

``` r
medianincome <- demographics %>%
  select(GEOID, hinc_18) %>%
  rename("Income in Dollars" = hinc_18)
incomejoin <-left_join(gfile, medianincome, by = "GEOID")
incomejoin
```

    ## # A tibble: 13 × 3
    ##         GEOID                                              geom `Income in Dol…`
    ##         <dbl>                                <MULTIPOLYGON [°]>            <dbl>
    ##  1 6075020800 (((-122.4217 37.7633, -122.4173 37.76357, -122.4…           103134
    ##  2 6075017700 (((-122.4187 37.77564, -122.4156 37.7731, -122.4…           114722
    ##  3 6075020700 (((-122.4261 37.76304, -122.4217 37.7633, -122.4…           167422
    ##  4 6075020100 (((-122.4226 37.7725, -122.4222 37.77291, -122.4…            46750
    ##  5 6075022801 (((-122.4173 37.76357, -122.4136 37.76382, -122.…           117368
    ##  6 6075022803 (((-122.4167 37.75717, -122.4078 37.75771, -122.…           123000
    ##  7 6075022903 (((-122.4093 37.7544, -122.4074 37.75451, -122.4…           128750
    ##  8 6075021000 (((-122.4254 37.75503, -122.421 37.75529, -122.4…           138523
    ##  9 6075022901 (((-122.4164 37.75397, -122.412 37.75423, -122.4…            91464
    ## 10 6075020200 (((-122.4269 37.76917, -122.4264 37.7696, -122.4…           100099
    ## 11 6075022802 (((-122.4084 37.76443, -122.4051 37.76463, -122.…           102750
    ## 12 6075020900 (((-122.421 37.75529, -122.4187 37.75544, -122.4…           106875
    ## 13 6075022902 (((-122.412 37.75423, -122.4093 37.7544, -122.40…           133239

``` r
medianincome_test <- demographics %>%
  select(GEOID, hinc_18) %>%
  mutate(median_income = case_when(
    hinc_18 <= 75000 ~ "40,000 - 75,000",
    hinc_18 >= 75001 & hinc_18 <= 110000 ~ "75,001 - 110,000",
    hinc_18 >= 110001 & hinc_18 <= 145000 ~ "110,001 - 145,000",
    hinc_18 >= 145001 ~ "145,001 - 180,000")) %>%
  rename("Income in Dollars" = hinc_18)
  #rename("Median Income" = median_income)
incomejoin_test <-left_join(gfile, medianincome_test, by = "GEOID")
incomejoin_test
```

    ## # A tibble: 13 × 4
    ##         GEOID                                geom `Income in Dol…` median_income
    ##         <dbl>                  <MULTIPOLYGON [°]>            <dbl> <chr>        
    ##  1 6075020800 (((-122.4217 37.7633, -122.4173 37…           103134 75,001 - 110…
    ##  2 6075017700 (((-122.4187 37.77564, -122.4156 3…           114722 110,001 - 14…
    ##  3 6075020700 (((-122.4261 37.76304, -122.4217 3…           167422 145,001 - 18…
    ##  4 6075020100 (((-122.4226 37.7725, -122.4222 37…            46750 40,000 - 75,…
    ##  5 6075022801 (((-122.4173 37.76357, -122.4136 3…           117368 110,001 - 14…
    ##  6 6075022803 (((-122.4167 37.75717, -122.4078 3…           123000 110,001 - 14…
    ##  7 6075022903 (((-122.4093 37.7544, -122.4074 37…           128750 110,001 - 14…
    ##  8 6075021000 (((-122.4254 37.75503, -122.421 37…           138523 110,001 - 14…
    ##  9 6075022901 (((-122.4164 37.75397, -122.412 37…            91464 75,001 - 110…
    ## 10 6075020200 (((-122.4269 37.76917, -122.4264 3…           100099 75,001 - 110…
    ## 11 6075022802 (((-122.4084 37.76443, -122.4051 3…           102750 75,001 - 110…
    ## 12 6075020900 (((-122.421 37.75529, -122.4187 37…           106875 75,001 - 110…
    ## 13 6075022902 (((-122.412 37.75423, -122.4093 37…           133239 110,001 - 14…

#### Figure 1.1: Mapping Median Household Income in the Mission District

Using **tmap** and our **incomejoin** table, we then create a map
showing median household income across census tracts in the Mission
District.

``` r
incomemap_2 <- tm_shape(incomejoin_test) +
             tm_style("watercolor") +
             tm_polygons("median_income") +
             tm_layout(main.title="Median Household Income",
                       main.title.position = "centre",
                       main.title.size = 1.6) +
             tm_legend(position = c("right", "top"),
             legend.outside = TRUE,
             legend.outside.size = .35,
             legend.title.size = 1.5,
             legend.text.size = 1.2) +
  tm_compass(position = c("left", "top"))
incomemap_2
```

![](Honors-Thesis-Workbook_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

## II Tract Racial Typology

To work with census data, we install **tidycensus** from CRAN with the
following command: `install.packages("tidycensus")`. After loading the
**tidycensus** and **tidyverse** libraries, obtain a [Census API
key](http://api.census.gov/data/key_signup.html). Note: 2020 decennial
Census data use differential privacy, a technique that introduces errors
into data to preserve respondent confidentiality, small counts should be
interpreted with caution.

``` r
census_api_key("77bb8e57772d9321db5adcd03b9bf2c3bce563c3", install = TRUE, overwrite = TRUE)
```

    ## [1] "77bb8e57772d9321db5adcd03b9bf2c3bce563c3"

#### Table 2.1 Population Numbers by Race

Using **tidycensus**, we will get the values for four variables: total
population, White population, Asian population, and Hispanic or Latino
population. The argument to the `geography` parameter is “tract”, and by
by specifying `state`, `county`, and `year` we get the desired
population numbers for each census tract in San Francisco from 2020.
Note that `geometry` is set to true in the first table to help create
maps later.

``` r
#White Population
white <- get_decennial(geography = "tract",
                      state = "CA",
                      county = "San Francisco",
                      year = 2020,
                      variables = c(white = "P1_003N"))
#Asian Population
asian <- get_decennial(geography = "tract",
                      state = "CA",
                      county = "San Francisco",
                      year = 2020,
                      variables = c(asian = "P1_006N"))
#Hispanic or Latino Population
latinx <- get_decennial(geography = "tract",
                      state = "CA",
                      county = "San Francisco",
                      year = 2020,
                      variables = c(latinx = "P2_002N"))
#Total Population
totalpop <- get_decennial(geography = "tract",
                      state = "CA",
                      county = "San Francisco",
                      year = 2020,
                      variables = c(totalpop = "P1_002N"),
                      geometry = TRUE)
```

    ##   |                                                                              |                                                                      |   0%  |                                                                              |                                                                      |   1%  |                                                                              |=                                                                     |   1%  |                                                                              |=                                                                     |   2%  |                                                                              |==                                                                    |   2%  |                                                                              |==                                                                    |   3%  |                                                                              |===                                                                   |   4%  |                                                                              |===                                                                   |   5%  |                                                                              |====                                                                  |   5%  |                                                                              |====                                                                  |   6%  |                                                                              |=====                                                                 |   7%  |                                                                              |=====                                                                 |   8%  |                                                                              |======                                                                |   8%  |                                                                              |======                                                                |   9%  |                                                                              |=======                                                               |   9%  |                                                                              |=======                                                               |  10%  |                                                                              |=======                                                               |  11%  |                                                                              |========                                                              |  11%  |                                                                              |=========                                                             |  12%  |                                                                              |=========                                                             |  13%  |                                                                              |==========                                                            |  14%  |                                                                              |==========                                                            |  15%  |                                                                              |===========                                                           |  16%  |                                                                              |============                                                          |  17%  |                                                                              |============                                                          |  18%  |                                                                              |=============                                                         |  19%  |                                                                              |==============                                                        |  20%  |                                                                              |===============                                                       |  21%  |                                                                              |===============                                                       |  22%  |                                                                              |================                                                      |  23%  |                                                                              |=================                                                     |  24%  |                                                                              |==================                                                    |  25%  |                                                                              |===================                                                   |  27%  |                                                                              |=========================                                             |  36%  |                                                                              |=============================                                         |  42%  |                                                                              |==================================                                    |  48%  |                                                                              |======================================                                |  54%  |                                                                              |==========================================                            |  60%  |                                                                              |==============================================                        |  65%  |                                                                              |==============================================                        |  66%  |                                                                              |==================================================                    |  72%  |                                                                              |======================================================                |  77%  |                                                                              |======================================================                |  78%  |                                                                              |===========================================================           |  84%  |                                                                              |===============================================================       |  90%  |                                                                              |===================================================================   |  96%  |                                                                              |======================================================================| 100%

#### Table 2.2: Race Percents

Next, with a series of `left_join`, we join the four previous tables by
“GEOID”. We `rename` and `select` several important variables for
neatness and clarity. We use `mutate` to add three columns displaying
the percentage of the total population that each race is.

``` r
totalandwhite <- left_join(totalpop, white, by = "GEOID") %>%
    rename(tract = NAME.x,
           totalvar = variable.x,
           totalval = value.x,
           whitevar = variable.y,
           whiteval = value.y) %>%
  select(GEOID, tract, totalvar, totalval, whitevar, whiteval)
asianandlatinx <- left_join(asian, latinx, by = "GEOID") %>%
    rename(tract = NAME.x,
           asianvar = variable.x,
           asianval = value.x,
           latinxvar = variable.y,
           latinxval = value.y) %>%
  select(GEOID, asianvar, asianval, latinxvar, latinxval)
racetable <- left_join(totalandwhite, asianandlatinx, by = "GEOID") %>%
  mutate(percwhite = (whiteval/totalval)*100) %>%
  mutate(percasian = (asianval/totalval)*100) %>%
  mutate(perclatinx = (latinxval/totalval)*100)
racetable
```

    ## # A tibble: 244 × 14
    ##    GEOID     tract totalvar totalval whitevar whiteval                  geometry
    ##    <chr>     <chr> <chr>       <dbl> <chr>       <dbl>        <MULTIPOLYGON [°]>
    ##  1 06075035… Cens… totalpop     3888 white        1957 (((-122.5099 37.76409, -…
    ##  2 06075040… Cens… totalpop     3936 white        2354 (((-122.4648 37.78856, -…
    ##  3 06075047… Cens… totalpop     3527 white        1582 (((-122.4887 37.77611, -…
    ##  4 06075026… Cens… totalpop     3852 white         260 (((-122.4113 37.71061, -…
    ##  5 06075012… Cens… totalpop     3088 white        1566 (((-122.4154 37.78932, -…
    ##  6 06075020… Cens… totalpop     3247 white        2238 (((-122.4352 37.76273, -…
    ##  7 06075021… Cens… totalpop     2620 white        2106 (((-122.4428 37.75238, -…
    ##  8 06075026… Cens… totalpop     2902 white         818 (((-122.4318 37.72825, -…
    ##  9 06075025… Cens… totalpop     4182 white         551 (((-122.4105 37.72849, -…
    ## 10 06075032… Cens… totalpop     3979 white        1553 (((-122.4848 37.76516, -…
    ## # … with 234 more rows, and 7 more variables: asianvar <chr>, asianval <dbl>,
    ## #   latinxvar <chr>, latinxval <dbl>, percwhite <dbl>, percasian <dbl>,
    ## #   perclatinx <dbl>

#### Table 2.3: Race Percents and Majorities

Next, we `mutate` to add a “majority” column. In this column, we use
`case_when` to show which of the three races has the highest percent of
the population, and thus, is the majority of its tract.

``` r
percents <- racetable  %>% 
  mutate(Majority = case_when(
    perclatinx > percasian & perclatinx > percwhite ~ "Hispanic or Latinx",
    percwhite > percasian & percwhite > perclatinx ~ "White",
    percasian > percwhite & percasian > perclatinx ~ "Asian")) %>%
  select(GEOID, tract, percwhite, percasian, perclatinx, Majority, geometry)
```

#### Table 2.4: Specifying the Boundaries

To narrow our scope, we then `filter` to only include census tracts in
the Mission District of San Francisco.

``` r
mission_geo_zero <- percents %>% pull(GEOID)
mission_percents_clean <- percents %>%
  mutate(GEOID = substring(mission_geo_zero, 2)) %>%
  filter(GEOID == "6075020201" | GEOID == "6075020202" | GEOID == "6075020101" | GEOID == "6075020102" | GEOID == "6075020801" | GEOID == "6075020802" | GEOID == "6075020701" | GEOID == "6075020702" | GEOID == "6075022902" | GEOID == "6075020900" | GEOID == "6075017700" | GEOID == "6075022901" | GEOID == "6075022803" | GEOID == "6075022903" | GEOID == "6075022801" | GEOID == "6075021000" | GEOID == "6075022802")
mission_percents_clean
```

    ## # A tibble: 17 × 7
    ##    GEOID tract percwhite percasian perclatinx Majority                  geometry
    ##    <chr> <chr>     <dbl>     <dbl>      <dbl> <chr>           <MULTIPOLYGON [°]>
    ##  1 6075… Cens…      41.7      25.2       35.5 White    (((-122.4226 37.7725, -1…
    ##  2 6075… Cens…      35.6      20.9       45.2 Hispani… (((-122.422 37.76654, -1…
    ##  3 6075… Cens…      72.8      14.3       18.0 White    (((-122.4258 37.75984, -…
    ##  4 6075… Cens…      44.4      17.8       49.4 Hispani… (((-122.421 37.75529, -1…
    ##  5 6075… Cens…      37.7      11.6       61.6 Hispani… (((-122.4164 37.75397, -…
    ##  6 6075… Cens…      38.0      18.8       54.5 Hispani… (((-122.4217 37.7633, -1…
    ##  7 6075… Cens…      51.9      24.1       29.9 White    (((-122.4265 37.76627, -…
    ##  8 6075… Cens…      48.8      17.1       47.8 White    (((-122.4093 37.7544, -1…
    ##  9 6075… Cens…      47.6      26.0       32.8 White    (((-122.4084 37.76443, -…
    ## 10 6075… Cens…      66.5      20.9       20.1 White    (((-122.4261 37.76304, -…
    ## 11 6075… Cens…      68.2      17.5       21.8 White    (((-122.4254 37.75503, -…
    ## 12 6075… Cens…      45.0      16.2       53.4 Hispani… (((-122.412 37.75423, -1…
    ## 13 6075… Cens…      44.9      19.6       46.9 Hispani… (((-122.4214 37.7601, -1…
    ## 14 6075… Cens…      46.2      23.2       30.2 White    (((-122.4187 37.77564, -…
    ## 15 6075… Cens…      48.3      17.3       41.6 White    (((-122.4173 37.76357, -…
    ## 16 6075… Cens…      52.7      26.1       25.8 White    (((-122.4269 37.76917, -…
    ## 17 6075… Cens…      46.5      15.4       51.5 Hispani… (((-122.4167 37.75717, -…

#### Figure 2.1: Mapping Racial Majorities in the Mission District

-   

``` r
racemap <-
  tm_shape(mission_percents_clean) +
  tm_polygons("Majority") +
  tm_style("watercolor") +
  tm_layout(main.title = "Racial Typography",
            main.title.position = "centre",
            main.title.size = 1.6) +
  tm_legend(position = c("right", "top"),
            legend.outside = TRUE,
            legend.outside.size = .35,
            legend.title.size = 1.5,
            legend.text.size = 1.2) +
  tm_compass(position = c("left", "top"))
racemap
```

![](Honors-Thesis-Workbook_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

## III Demographics Table

#### Table 3.1

``` r
incomejoin_chr <- incomejoin %>%
  mutate_at("GEOID", as.character)
incomejoin_chr
```

    ## # A tibble: 13 × 3
    ##    GEOID                                                   geom `Income in Dol…`
    ##    <chr>                                     <MULTIPOLYGON [°]>            <dbl>
    ##  1 6075020800 (((-122.4217 37.7633, -122.4173 37.76357, -122.4…           103134
    ##  2 6075017700 (((-122.4187 37.77564, -122.4156 37.7731, -122.4…           114722
    ##  3 6075020700 (((-122.4261 37.76304, -122.4217 37.7633, -122.4…           167422
    ##  4 6075020100 (((-122.4226 37.7725, -122.4222 37.77291, -122.4…            46750
    ##  5 6075022801 (((-122.4173 37.76357, -122.4136 37.76382, -122.…           117368
    ##  6 6075022803 (((-122.4167 37.75717, -122.4078 37.75771, -122.…           123000
    ##  7 6075022903 (((-122.4093 37.7544, -122.4074 37.75451, -122.4…           128750
    ##  8 6075021000 (((-122.4254 37.75503, -122.421 37.75529, -122.4…           138523
    ##  9 6075022901 (((-122.4164 37.75397, -122.412 37.75423, -122.4…            91464
    ## 10 6075020200 (((-122.4269 37.76917, -122.4264 37.7696, -122.4…           100099
    ## 11 6075022802 (((-122.4084 37.76443, -122.4051 37.76463, -122.…           102750
    ## 12 6075020900 (((-122.421 37.75529, -122.4187 37.75544, -122.4…           106875
    ## 13 6075022902 (((-122.412 37.75423, -122.4093 37.7544, -122.40…           133239

#### Table 3.2: Demographics Table

``` r
finaljoin <- right_join(st_drop_geometry(incomejoin_chr), st_drop_geometry(mission_percents_clean), by = "GEOID") %>% 
  select(GEOID, tract, "Income in Dollars", Majority, percwhite, perclatinx, percasian) %>% 
  rename("Median Income ($)" = "Income in Dollars", Tract = tract, "White Percentage" = percwhite, "Hispanic/Latinx Percentage" = perclatinx, "Asian Percentage" = percasian, "Racial Majority" = Majority)
finaljoin
```

    ## # A tibble: 17 × 7
    ##    GEOID      Tract           `Median Income…` `Racial Majori…` `White Percent…`
    ##    <chr>      <chr>                      <dbl> <chr>                       <dbl>
    ##  1 6075017700 Census Tract 1…           114722 White                        46.2
    ##  2 6075022801 Census Tract 2…           117368 White                        48.3
    ##  3 6075022803 Census Tract 2…           123000 Hispanic or Lat…             46.5
    ##  4 6075022903 Census Tract 2…           128750 White                        48.8
    ##  5 6075021000 Census Tract 2…           138523 White                        68.2
    ##  6 6075022901 Census Tract 2…            91464 Hispanic or Lat…             37.7
    ##  7 6075022802 Census Tract 2…           102750 White                        47.6
    ##  8 6075020900 Census Tract 2…           106875 Hispanic or Lat…             44.4
    ##  9 6075022902 Census Tract 2…           133239 Hispanic or Lat…             45.0
    ## 10 6075020101 Census Tract 2…               NA White                        41.7
    ## 11 6075020102 Census Tract 2…               NA Hispanic or Lat…             35.6
    ## 12 6075020701 Census Tract 2…               NA White                        72.8
    ## 13 6075020802 Census Tract 2…               NA Hispanic or Lat…             38.0
    ## 14 6075020201 Census Tract 2…               NA White                        51.9
    ## 15 6075020702 Census Tract 2…               NA White                        66.5
    ## 16 6075020801 Census Tract 2…               NA Hispanic or Lat…             44.9
    ## 17 6075020202 Census Tract 2…               NA White                        52.7
    ## # … with 2 more variables: `Hispanic/Latinx Percentage` <dbl>,
    ## #   `Asian Percentage` <dbl>

## IV Food Retailers

#### Table 4.1: Uploading business data from data.sfgov.org.

``` r
SF_businesses <- read_csv("https://data.sfgov.org/api/views/g8m3-pdis/rows.csv?accessType=DOWNLOAD")
```

    ## Rows: 288046 Columns: 32
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (24): Location Id, Business Account Number, Ownership Name, DBA Name, St...
    ## dbl  (6): Supervisor District, SF Find Neighborhoods, Current Police Distric...
    ## lgl  (2): Parking Tax, Transient Occupancy Tax
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
SF_businesses
```

    ## # A tibble: 288,046 × 32
    ##    `Location Id`  `Business Accou…` `Ownership Name` `DBA Name` `Street Address`
    ##    <chr>          <chr>             <chr>            <chr>      <chr>           
    ##  1 1014347-12-141 0077021           Abm Industries … Ampco Sys… 600 Montgomery …
    ##  2 1014379-12-141 0077021           Abm Industries … Ampco Sys… 501 Post St     
    ##  3 0030032-46-001 0030032           Walgreen Co      Walgreens… 845 Market St   
    ##  4 0088595-01-001 0088595           Spano Robert & … 282-290 C… 282 Clipper St  
    ##  5 0028703-02-001 0028703           Vericlaim Inc    Vericlaim… 500 Sansome St …
    ##  6 1012834-11-141 0091116           Urban Land Serv… Urban Lan… 1170 Sacramento…
    ##  7 0348331-01-001 0348331           Tran Sandy Dung  Elizabeth… 672 Geary St    
    ##  8 0331802-01-001 0331802           Ken Chi Chuan A… Ken Chi C… 3626 Taraval St…
    ##  9 0124761-06-001 0124761           Vaccaro Joseph … 119 Day S… 119 Day St      
    ## 10 1243902-01-201 0306019           Shatara Suheil E Shatara A… 60 Divisadero St
    ## # … with 288,036 more rows, and 27 more variables: City <chr>, State <chr>,
    ## #   `Source Zipcode` <chr>, `Business Start Date` <chr>,
    ## #   `Business End Date` <chr>, `Location Start Date` <chr>,
    ## #   `Location End Date` <chr>, `Mail Address` <chr>, `Mail City` <chr>,
    ## #   `Mail Zipcode` <chr>, `Mail State` <chr>, `NAICS Code` <chr>,
    ## #   `NAICS Code Description` <chr>, `Parking Tax` <lgl>,
    ## #   `Transient Occupancy Tax` <lgl>, `LIC Code` <chr>, …

#### Table 4.2: Business in the Mission with LIC Code H in it. LIC codes with H’s are retail businesses, this was a crucial filtering step to finding food retailers.

``` r
Mission_H_Codes <- SF_businesses %>%
   filter(str_detect(`LIC Code`, "H"), `Neighborhoods - Analysis Boundaries` == "Mission") %>%
  select(`Ownership Name`, `DBA Name`, `Street Address`, `Business Start Date`, `Business End Date`, `Mail State`, `NAICS Code`, `NAICS Code Description`, `LIC Code`, `LIC Code Description`, `Neighborhoods - Analysis Boundaries`)
Mission_H_Codes %>% select(`Ownership Name`, `DBA Name`, `LIC Code`, `LIC Code Description`)
```

    ## # A tibble: 983 × 4
    ##    `Ownership Name`              `DBA Name`          `LIC Code` `LIC Code Desc…`
    ##    <chr>                         <chr>               <chr>      <chr>           
    ##  1 Leigh Wendy A                 Listening Hands Ma… H68        General Massage…
    ##  2 Walgreen Co                   Walgreens #03711    H05 Pos01… Multiple        
    ##  3 Walgreen Co                   Walgreens #09886    H04 Pos01… Multiple        
    ##  4 Walgreen Co                   Walgreen Co         H83        Supermarkets W/…
    ##  5 Rtrn Investment Llc           Travelodge Central  Hhh        <NA>            
    ##  6 Dai Shujuan/altamirano Carlos Sanguchon           H25        Restaurant 1,00…
    ##  7 Chu Edwin W Y & Priscilla P C E P Laundromat      H46        Auto Laundry Me…
    ##  8 Telli Tim                     Betwixt Wines       H73        Deemed Approved…
    ##  9 Naran Mangu                   Frances Hotel       Hhh        <NA>            
    ## 10 Pan O Rama Baking Inc         Pan-O-Rama          H30        Catering Facili…
    ## # … with 973 more rows

#### List 4.1: The following is a list of LIC codes that are food retailers. This list includes grocery stores, corner markets, convienence stores, supermarkets, bakeries, and drug stores. This list does not include restaurants.

``` r
H_strings <- c("H01", "H02", "H03", "H04", "H05", "H06", "H07", "H08", "H09", "H10", "H11", "H12", "H13", "H14", "H16", "H19", "H80", "H81", "H83", "H88", "H89", "H92")
```

#### Table 4.3: The follow is a table that includes data on all food retailers within the Mission District.

``` r
Final_Mission_Food_Retailers <- SF_businesses %>%
  filter(`Neighborhoods - Analysis Boundaries` == "Mission") %>%
  filter(str_detect(`LIC Code`, paste(H_strings, collapse = "|")))
Final_Mission_Food_Retailers
```

    ## # A tibble: 147 × 32
    ##    `Location Id`  `Business Accou…` `Ownership Name` `DBA Name` `Street Address`
    ##    <chr>          <chr>             <chr>            <chr>      <chr>           
    ##  1 0030032-06-001 0030032           Walgreen Co      Walgreens… 1189 Potrero Ave
    ##  2 0030032-40-001 0030032           Walgreen Co      Walgreens… 3400 Cesar Chav…
    ##  3 0030032-01-015 0030032           Walgreen Co      Walgreen … 1979 Mission St 
    ##  4 1021716-03-151 1010484           Yangtze Market … Yangtze M… 2026 Mission St 
    ##  5 0069288-01-001 0069288           Samiramis Impor… Samiramis… 2990 Mission St 
    ##  6 0303375-02-001 0303375           Karajah Kamel F  Smoke Time 2733 Mission St 
    ##  7 0090813-01-001 0090813           Rainbow Grocery… Rainbow G… 1745 Folsom St  
    ##  8 1201886-10-181 1093331           Karla Garcia     Bris's Cr… 2782 24th St    
    ##  9 0108305-01-001 0108305           Totah B/totah M… Norms Mar… 2201 Bryant St  
    ## 10 0320117-01-001 0320117           Fadhel Hizam A   George's … 2268 Mission St 
    ## # … with 137 more rows, and 27 more variables: City <chr>, State <chr>,
    ## #   `Source Zipcode` <chr>, `Business Start Date` <chr>,
    ## #   `Business End Date` <chr>, `Location Start Date` <chr>,
    ## #   `Location End Date` <chr>, `Mail Address` <chr>, `Mail City` <chr>,
    ## #   `Mail Zipcode` <chr>, `Mail State` <chr>, `NAICS Code` <chr>,
    ## #   `NAICS Code Description` <chr>, `Parking Tax` <lgl>,
    ## #   `Transient Occupancy Tax` <lgl>, `LIC Code` <chr>, …

``` r
Clean_Final_Retail <- Final_Mission_Food_Retailers %>%
  select("Ownership Name", "DBA Name", "Street Address", "LIC Code Description")
Clean_Final_Retail
```

    ## # A tibble: 147 × 4
    ##    `Ownership Name`         `DBA Name`         `Street Address` `LIC Code Desc…`
    ##    <chr>                    <chr>              <chr>            <chr>           
    ##  1 Walgreen Co              Walgreens #03711   1189 Potrero Ave Multiple        
    ##  2 Walgreen Co              Walgreens #09886   3400 Cesar Chav… Multiple        
    ##  3 Walgreen Co              Walgreen Co        1979 Mission St  Supermarkets W/…
    ##  4 Yangtze Market Inc       Yangtze Market     2026 Mission St  Multiple        
    ##  5 Samiramis Imports Inc    Samiramis Imports… 2990 Mission St  Multiple        
    ##  6 Karajah Kamel F          Smoke Time         2733 Mission St  Multiple        
    ##  7 Rainbow Grocery Inc      Rainbow Grocery C… 1745 Folsom St   Multiple        
    ##  8 Karla Garcia             Bris's Creations   2782 24th St     Retail Bakeries…
    ##  9 Totah B/totah M/ Totah N Norms Market       2201 Bryant St   Multiple        
    ## 10 Fadhel Hizam A           George's Market    2268 Mission St  Multiple        
    ## # … with 137 more rows

``` r
Clean_Order_r <- Clean_Final_Retail[order(Clean_Final_Retail$"DBA Name"),]
Clean_Order_r
```

    ## # A tibble: 147 × 4
    ##    `Ownership Name`                 `DBA Name` `Street Address` `LIC Code Desc…`
    ##    <chr>                            <chr>      <chr>            <chr>           
    ##  1 Binaya Pokharel And Mandira Shr… 23rd & Gu… 3558 23rd St     Retail Food Mar…
    ##  2 Samra Bros Inc                   26th & Gu… 1400 Guerrero St Multiple        
    ##  3 Shehadeh Nizar A                 Abc Market 2801 Bryant St   Multiple        
    ##  4 Mosleh Hamood                    All Seaso… 401 Capp St      Multiple        
    ##  5 All Season Market                All Seaso… 401 Capp St      Multiple        
    ##  6 Cervantes Marisa                 All Star … 3350 18th St     Retail Mkts W/o…
    ##  7 Anthony's Cookies Inc            Anthony's… 1417 Valencia St Retail Bakeries…
    ##  8 Elias Carmen                     Bakery La… 3329 24th St     Retail Bakeries…
    ##  9 Lai Hung Dat                     Basa Seaf… 3064 24th St     Multiple        
    ## 10 Best Buy Stores, L.p.            Best Buy … 1717 Harrison St Retail Mkts W/o…
    ## # … with 137 more rows

``` r
write.csv(Clean_Order_r, "C:\\Users\\fheim\\Desktop\\Test\\People.csv", row.names = FALSE)
```

#### List 4.2: The following are the coordinates for each food retail store in the Mission District.

``` r
coordinates <- Final_Mission_Food_Retailers %>% pull("Business Location")
coordinates
```

    ##   [1] "POINT (-122.40632 37.75321)"   "POINT (-122.41832 37.74822)"  
    ##   [3] "POINT (-122.41967 37.765438)"  "POINT (-122.419655 37.764576)"
    ##   [5] "POINT (-122.41819 37.749245)"  "POINT (-122.41851 37.753284)" 
    ##   [7] "POINT (-122.415565 37.76945)"  "POINT (-122.407875 37.7529)"  
    ##   [9] "POINT (-122.409706 37.759117)" "POINT (-122.41929 37.760757)" 
    ##  [11] "POINT (-122.41885 37.761894)"  "POINT (-122.421074 37.756813)"
    ##  [13] "POINT (-122.41839 37.76192)"   "POINT (-122.42002 37.768364)" 
    ##  [15] "POINT (-122.417435 37.765038)" "POINT (-122.41564 37.768444)" 
    ##  [17] "POINT (-122.41881 37.756397)"  "POINT (-122.41992 37.75566)"  
    ##  [19] "POINT (-122.413284 37.75258)"  "POINT (-122.416374 37.75388)" 
    ##  [21] "POINT (-122.4215 37.773273)"   "POINT (-122.4189 37.75739)"   
    ##  [23] "POINT (-122.41954 37.763336)"  "POINT (-122.41356 37.757385)" 
    ##  [25] "POINT (-122.41375 37.749424)"  "POINT (-122.407974 37.75289)" 
    ##  [27] "POINT (-122.409706 37.757614)" "POINT (-122.41925 37.760323)" 
    ##  [29] "POINT (-122.41888 37.757126)"  "POINT (-122.417305 37.763664)"
    ##  [31] "POINT (-122.41939 37.761745)"  "POINT (-122.42239 37.769775)" 
    ##  [33] "POINT (-122.418625 37.75451)"  "POINT (-122.41841 37.751568)" 
    ##  [35] "POINT (-122.41398 37.75254)"   "POINT (-122.41015 37.757587)" 
    ##  [37] "POINT (-122.40704 37.75295)"   "POINT (-122.424324 37.771053)"
    ##  [39] "POINT (-122.42416 37.764698)"  "POINT (-122.419365 37.762287)"
    ##  [41] "POINT (-122.421844 37.764828)" "POINT (-122.4194 37.76195)"   
    ##  [43] "POINT (-122.42307 37.755203)"  "POINT (-122.40898 37.752777)" 
    ##  [45] "POINT (-122.41286 37.752605)"  "POINT (-122.41554 37.76978)"  
    ##  [47] "POINT (-122.4095 37.756077)"   "POINT (-122.41369 37.771557)" 
    ##  [49] "POINT (-122.41973 37.766026)"  "POINT (-122.40878 37.74951)"  
    ##  [51] "POINT (-122.4091 37.761597)"   "POINT (-122.42372 37.760036)" 
    ##  [53] "POINT (-122.42044 37.750187)"  "POINT (-122.40623 37.751453)" 
    ##  [55] "POINT (-122.419495 37.762894)" "POINT (-122.4074 37.752872)"  
    ##  [57] "POINT (-122.41949 37.76355)"   "POINT (-122.42087 37.753963)" 
    ##  [59] "POINT (-122.42263 37.74869)"   "POINT (-122.42023 37.755314)" 
    ##  [61] "POINT (-122.41925 37.760323)"  "POINT (-122.42011 37.765053)" 
    ##  [63] "POINT (-122.42105 37.75585)"   "POINT (-122.42093 37.752323)" 
    ##  [65] "POINT (-122.416695 37.75726)"  "POINT (-122.41445 37.75251)"  
    ##  [67] "POINT (-122.40836 37.75287)"   "POINT (-122.414345 37.75561)" 
    ##  [69] "POINT (-122.42145 37.76001)"   "POINT (-122.418526 37.75276)" 
    ##  [71] "POINT (-122.41607 37.74919)"   "POINT (-122.418465 37.752823)"
    ##  [73] "POINT (-122.417244 37.752285)" "POINT (-122.41346 37.76908)"  
    ##  [75] "POINT (-122.411125 37.752647)" "POINT (-122.40952 37.76569)"  
    ##  [77] "POINT (-122.41865 37.75404)"   "POINT (-122.42064 37.752197)" 
    ##  [79] "POINT (-122.41829 37.750965)"  "POINT (-122.423904 37.76325)" 
    ##  [81] "POINT (-122.422585 37.764847)" "POINT (-122.418236 37.750435)"
    ##  [83] "POINT (-122.41901 37.765118)"  "POINT (-122.42069 37.75201)"  
    ##  [85] "POINT (-122.41862 37.753746)"  "POINT (-122.418106 37.749134)"
    ##  [87] "POINT (-122.41337 37.769302)"  "POINT (-122.40952 37.76569)"  
    ##  [89] "POINT (-122.42011 37.765053)"  "POINT (-122.41859 37.7541)"   
    ##  [91] "POINT (-122.41085 37.75272)"   "POINT (-122.418076 37.760212)"
    ##  [93] "POINT (-122.41029 37.763206)"  "POINT (-122.419174 37.752167)"
    ##  [95] "POINT (-122.42202 37.766632)"  "POINT (-122.413185 37.752586)"
    ##  [97] "POINT (-122.42101 37.764942)"  "POINT (-122.42132 37.758614)" 
    ##  [99] "POINT (-122.42338 37.7584)"    "POINT (-122.41043 37.752743)" 
    ## [101] "POINT (-122.41397 37.75102)"   "POINT (-122.421265 37.7581)"  
    ## [103] "POINT (-122.40952 37.76569)"   "POINT (-122.417694 37.753918)"
    ## [105] "POINT (-122.41959 37.76464)"   "POINT (-122.419075 37.75854)" 
    ## [107] "POINT (-122.41124 37.754307)"  "POINT (-122.40866 37.75285)"  
    ## [109] "POINT (-122.40747 37.76469)"   "POINT (-122.407974 37.75289)" 
    ## [111] "POINT (-122.40924 37.766758)"  "POINT (-122.41631 37.753246)" 
    ## [113] "POINT (-122.4185 37.752502)"   "POINT (-122.41861 37.77296)"  
    ## [115] "POINT (-122.41933 37.75216)"   "POINT (-122.41851 37.760303)" 
    ## [117] "POINT (-122.4181 37.755505)"   "POINT (-122.41066 37.75273)"  
    ## [119] "POINT (-122.42258 37.772312)"  "POINT (-122.40805 37.75927)"  
    ## [121] "POINT (-122.40649 37.75299)"   "POINT (-122.40399 37.7544)"   
    ## [123] "POINT (-122.411316 37.752636)" "POINT (-122.41262 37.760426)" 
    ## [125] "POINT (-122.41827 37.750732)"  "POINT (-122.422005 37.76494)" 
    ## [127] "POINT (-122.412025 37.770237)" "POINT (-122.41294 37.763786)" 
    ## [129] "POINT (-122.41862 37.753685)"  "POINT (-122.41903 37.758755)" 
    ## [131] "POINT (-122.42076 37.76501)"   "POINT (-122.422226 37.768047)"
    ## [133] "POINT (-122.4058 37.754288)"   "POINT (-122.42109 37.756992)" 
    ## [135] "POINT (-122.41724 37.74907)"   "POINT (-122.42077 37.752857)" 
    ## [137] "POINT (-122.423744 37.76165)"  "POINT (-122.418076 37.760212)"
    ## [139] "POINT (-122.415054 37.75242)"  "POINT (-122.42084 37.753613)" 
    ## [141] "POINT (-122.41816 37.74895)"   "POINT (-122.410484 37.75591)" 
    ## [143] "POINT (-122.42239 37.753635)"  "POINT (-122.41724 37.74907)"  
    ## [145] "POINT (-122.41888 37.757126)"  "POINT (-122.42416 37.764698)" 
    ## [147] "POINT (-122.424324 37.771053)"

#### Figure 4.1: The follow is a map of all food retailers within the Mission District. Each dot represents a food retailer. While this map does not include streets or the outline of the Mission Distict, maps in the following section will include an outline of the Mission District along with demographic information.

-   

``` r
geo_final <- Final_Mission_Food_Retailers %>%
  rename(geometry = `Business Location`) %>%
  mutate(geometry = as.list(geometry)) %>%
  st_as_sf(crs = "WGS84")
tm_shape(geo_final) + tm_dots()
```

![](Honors-Thesis-Workbook_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

``` r
retail_data <- read_csv("Food Retail Final List (Edit 3_30).csv")
```

    ## New names:
    ## * `` -> ...46

    ## Rows: 97 Columns: 49
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (35): Timestamp, Name of Food Retailer, Address, Date Assessed, Type of ...
    ## dbl (12): Median Price of a Dozen Eggs, Median Price of a Loaf of Bread, Mil...
    ## lgl  (1): ...46
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
retail_data$coord <- paste(retail_data$lon, retail_data$lat)
retail_data
```

    ## # A tibble: 97 × 50
    ##    Timestamp       `Name of Food Retai…` Address `Date Assessed` `Type of Store`
    ##    <chr>           <chr>                 <chr>   <chr>           <chr>          
    ##  1 1/27/2022 12:38 Mission Foodhall      3100 1… 1/26/2022       Specialty Food…
    ##  2 1/27/2022 12:41 Fred’s Liquors & Del… 200 Va… 1/26/2022       Grocery Store  
    ##  3 1/27/2022 12:43 E And M Market        399 Va… 1/26/2022       Convenience St…
    ##  4 1/27/2022 12:46 K & H Liquor          501 Va… 1/26/2022       Convenience St…
    ##  5 1/27/2022 12:48 Valencia Whole Foods  999 Va… 1/26/2022       Grocery Store  
    ##  6 1/27/2022 12:50 Decamere Market       1001 V… 1/26/2022       Convenience St…
    ##  7 1/27/2022 12:52 Indian Spices and Gr… 3265 2… 1/26/2022       Specialty Food…
    ##  8 1/27/2022 12:55 Valencia Farmer’s Ma… 1299 V… 1/26/2022       Grocery Store  
    ##  9 1/27/2022 12:59 Valencia Grocery      1300 V… 1/26/2022       Convenience St…
    ## 10 1/27/2022 13:02 Mr. Liquor            1200 V… 1/26/2022       Convenience St…
    ## # … with 87 more rows, and 45 more variables:
    ## #   `What type of Specialty Food Store?` <chr>, `EBT Accepted?` <chr>,
    ## #   `Number of Locations (chain?)` <dbl>, `Median Price of a Dozen Eggs` <dbl>,
    ## #   `Median Price of a Loaf of Bread` <dbl>,
    ## #   `Median Price of a Gallon of Milk` <chr>, `Milk Standardized_Gallon` <dbl>,
    ## #   `Median Price of Oranges` <chr>, `Orange Standardized_lbs` <dbl>,
    ## #   `Median Price of Organic Oranges` <chr>, …

``` r
retail_map <- retail_data %>%
 st_as_sf(coords = c('lon', 'lat'), crs = "WGS84")
tm_shape(retail_map) + tm_dots()
```

![](Honors-Thesis-Workbook_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

## V Final Maps

#### Figure 5.1: Food Retailers and Median Household Income in the Mission District

``` r
dots <- tm_shape(retail_map) + tm_dots(col="black") + tm_add_legend(shape = "tm_dots", labels = ('Food Retailers'), col = "black")
incomemap_with_food_retailers <- tm_shape(incomejoin_test) +
             tm_style("watercolor") +
             tm_polygons("median_income") +
             tm_layout(main.title="Median Household Income & Food Retailers",
                       main.title.position = "centre",
                       main.title.size = 1.6) +
             tm_legend(position = c("right", "top"),
             legend.outside = TRUE,
             legend.outside.size = .35,
             legend.title.size = 1.5,
             legend.text.size = 1.2) +
  tm_compass(position = c("left", "top"))
income_map_with_retail <- incomemap_with_food_retailers + dots
income_map_with_retail
```

![](Honors-Thesis-Workbook_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->

#### Figure 5.2: Food Retailers and Racial Majorities in the Mission District

-   

``` r
dots <- tm_shape(retail_map) + tm_dots(col="black") + tm_add_legend(shape = "tm_dots", labels = ('Food Retailers'), col = "black")
racemap_with_food_retailers <-
  tm_shape(mission_percents_clean) +
  tm_polygons("Majority") +
  tm_style("watercolor") +
  tm_layout(main.title = "Racial Typography & Food Retailers",
            main.title.position = "centre",
            main.title.size = 1.6) +
  tm_legend(position = c("right", "top"),
            legend.outside = TRUE,
            legend.outside.size = .35,
            legend.title.size = 1.5,
            legend.text.size = 1.2) +
  tm_compass(position = c("left", "top"))
ethnicity_with_retail <- racemap_with_food_retailers + dots
ethnicity_with_retail
```

![](Honors-Thesis-Workbook_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->

# Conclusion

We were able to create maps of the Mission District based off median
household income, racial majorities, and the distribution of food
retailers. First, our map displaying median household income
demonstrates the income gap experienced in the Mission today. Median
income in tracts ranged from 40,000-60,000 USD on the lower end, to
160,000-180,000 USD on the upper end, with five other ranges in between.
The lowest and highest median income tracts share a corner in the
Northwestern quadrant of the Mission, demonstrating the proximity of the
income gap in the Mission District.

Our racial typography map revealed that Hispanic or Latinx and White are
the majority races in the Mission District. There are ten tracts that
were predominantly white and seven tracts that are predominantly
Hispanic or Latinx. These findings demonstrate that a degree of racial
diversity exists in the Mission District, albeit largely between two
races. If you compare the Median Household Income map with the Racial
Typography map it is apparent that there is some degree of correlation
between lower-income census tracts and tracts that are predominately
Hispanic/Latinx. This may be an important trend when researching levels
of gentrification within the Mission District. However, while our
findings display that there is a degree of racial integration within the
Mission District, they do not reveal the degree of segregation occurring
within each tact. Further research would be needed to understand the
landscape of segregation within each tract.

When we examined the socio-economic landscape of the Mission District in
relation to the distribution of food retailers, we observed that there
seems to be a level of correlation between the number of food retailers
and tracts that are predominantly Hispanic and Latinx. If the maps we
generated are compared to street maps (we direct readers to use Google
Maps or other mapping software), the majority of food retailers are
located along Mission Street and 24th Street–both streets are hubs for
Latinx populations and culture. Our Racial Typography & Food Retailers
map exemplifies that there may be a correlation between the location and
quantity of food retailers in the Mission District and racial majority;
however, our Median Household Income & Food Retailers map doesn’t
demonstrate the same level of correlation. In the later case, the
location of food retailers may have more to do with business corridors
than median household income distribution.

In conclusion, we were able to replicate multiple maps used in
researching the socio-economic landscapes of the Mission District. We
were then able to start research, and open a discussion, about how this
correlates with the distribution of food retailers within the district.
Our work should be scene as a catalyst for future research on the food
retail landscape of the Mission District. For example, it should be
stated that in our maps all food retailers–regardless of size, stock, or
purpose–are resembled by a single black dot. However, there is great
diversity among food retailers. Some may be supermarkets, convenience
stores, or corner markets. Additionally, some may cater to the general
public, while others may sell specialty or ethnic foods. These kinds of
differences would be important to know before drawing any conclusions
regarding the distribution of food retailers in the Mission District in
relation to socio-economic landscapes. Using our research as a launching
pad, it is our hope that researches take our findings and code to
further examine the role of food retailers in the socio-economic fabric
of the Mission District.

\#Research Data (DRAFT)

``` r
retail_data <- read_csv("Food Retail Final List (Edit 3_30).csv") %>%
  select(!"Timestamp")
```

    ## New names:
    ## * `` -> ...46

    ## Rows: 97 Columns: 49
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (35): Timestamp, Name of Food Retailer, Address, Date Assessed, Type of ...
    ## dbl (12): Median Price of a Dozen Eggs, Median Price of a Loaf of Bread, Mil...
    ## lgl  (1): ...46
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
retail_data$coord <- paste(retail_data$lon, retail_data$lat) 
retail_data
```

    ## # A tibble: 97 × 49
    ##    `Name of Food Reta…` Address `Date Assessed` `Type of Store` `What type of …`
    ##    <chr>                <chr>   <chr>           <chr>           <chr>           
    ##  1 Mission Foodhall     3100 1… 1/26/2022       Specialty Food… Foodhall        
    ##  2 Fred’s Liquors & De… 200 Va… 1/26/2022       Grocery Store   <NA>            
    ##  3 E And M Market       399 Va… 1/26/2022       Convenience St… <NA>            
    ##  4 K & H Liquor         501 Va… 1/26/2022       Convenience St… <NA>            
    ##  5 Valencia Whole Foods 999 Va… 1/26/2022       Grocery Store   <NA>            
    ##  6 Decamere Market      1001 V… 1/26/2022       Convenience St… <NA>            
    ##  7 Indian Spices and G… 3265 2… 1/26/2022       Specialty Food… Ethnic Store    
    ##  8 Valencia Farmer’s M… 1299 V… 1/26/2022       Grocery Store   <NA>            
    ##  9 Valencia Grocery     1300 V… 1/26/2022       Convenience St… <NA>            
    ## 10 Mr. Liquor           1200 V… 1/26/2022       Convenience St… <NA>            
    ## # … with 87 more rows, and 44 more variables: `EBT Accepted?` <chr>,
    ## #   `Number of Locations (chain?)` <dbl>, `Median Price of a Dozen Eggs` <dbl>,
    ## #   `Median Price of a Loaf of Bread` <dbl>,
    ## #   `Median Price of a Gallon of Milk` <chr>, `Milk Standardized_Gallon` <dbl>,
    ## #   `Median Price of Oranges` <chr>, `Orange Standardized_lbs` <dbl>,
    ## #   `Median Price of Organic Oranges` <chr>,
    ## #   `Organic Oranges Standardized_lbs` <dbl>, …

``` r
dots <- tm_shape(retail_map) + tm_dots(col="EBT Accepted?", palette=c(No='red', Yes='black'))
incomemap_with_food_retailers <- tm_shape(incomejoin_test) +
             tm_style("watercolor") +
             tm_polygons("median_income") +
             tm_layout(main.title="Median Household Income & Food Retailers",
                       main.title.position = "centre",
                       main.title.size = 1.6) +
             tm_legend(position = c("right", "top"),
             legend.outside = TRUE,
             legend.outside.size = .35,
             legend.title.size = 1.5,
             legend.text.size = 1.2) +
  tm_compass(position = c("left", "top"))
income_plus_points <- incomemap_with_food_retailers + dots
income_plus_points
```

![](Honors-Thesis-Workbook_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->

\##\`\`\`{r} intersection \<- st_intersection(x =
incomemap_with_food_retailers$median_income, y = dots) class(retail_map)
\# Plot intersection plot(polygon, graticule = st_crs(4326), key.pos
= 1) plot(intersection\[1\], col = “black”, pch = 19, add = TRUE)

# View result

table(intersection$id_polygons) \# using table

# using dplyr

int_result \<- intersection %\>% group_by(id_polygons) %\>% count()

as.data.frame(int_result)\[,-3\]

\##\`\`\`

``` r
retail_EBT <- retail_map %>%
  filter(`EBT Accepted?` == "Yes")
retail_EBT
```

    ## # A tibble: 58 × 49
    ##    Timestamp       `Name of Food Retai…` Address `Date Assessed` `Type of Store`
    ##    <chr>           <chr>                 <chr>   <chr>           <chr>          
    ##  1 1/27/2022 12:43 E And M Market        399 Va… 1/26/2022       Convenience St…
    ##  2 1/27/2022 12:48 Valencia Whole Foods  999 Va… 1/26/2022       Grocery Store  
    ##  3 1/28/2022 11:09 Guerrero Hill Market  3398 2… 1/26/2022       Convenience St…
    ##  4 1/28/2022 12:30 Walgreens             2690 M… 1/28/2022       Supermarket    
    ##  5 1/28/2022 12:43 23rd & Mission Produ… 2700 M… 1/28/2022       Grocery Store  
    ##  6 1/28/2022 13:01 Casa Maria Produce M… 1201 S… 1/28/2022       Grocery Store  
    ##  7 1/28/2022 13:20 Grocery Outlet        1245 S… 1/28/2022       Supermarket    
    ##  8 2/9/2022 13:16  New Star Market Liqu… 269 14… 2/9/2022        Convenience St…
    ##  9 2/9/2022 13:25  S & M Liquor & Market 1939 M… 2/9/2022        Convenience St…
    ## 10 2/9/2022 13:32  Hwa Lei Market        2970 1… 2/9/2022        Grocery Store  
    ## # … with 48 more rows, and 44 more variables:
    ## #   `What type of Specialty Food Store?` <chr>, `EBT Accepted?` <chr>,
    ## #   `Number of Locations (chain?)` <dbl>, `Median Price of a Dozen Eggs` <dbl>,
    ## #   `Median Price of a Loaf of Bread` <dbl>,
    ## #   `Median Price of a Gallon of Milk` <chr>, `Milk Standardized_Gallon` <dbl>,
    ## #   `Median Price of Oranges` <chr>, `Orange Standardized_lbs` <dbl>,
    ## #   `Median Price of Organic Oranges` <chr>, …

``` r
#income
just_geo <- incomejoin_test %>%
  select("geom")
just_mission_stores <- retail_map %>%
  filter(`Name of Food Retailer` != "Costco") %>%
  filter(`Name of Food Retailer` != "Whole Foods Market") %>%
  filter(`Address` != "2020 Market St, San Francisco, CA 94114")

intersection <- st_intersection(x = just_geo, y = just_mission_stores)
```

    ## Warning: attribute variables are assumed to be spatially constant throughout all
    ## geometries

``` r
intersection_join <- st_join(intersection, incomejoin_test, join = st_intersects)
intersection_join
```

    ## # A tibble: 94 × 52
    ##    Timestamp       Name.of.Food.Retailer     Address Date.Assessed Type.of.Store
    ##    <chr>           <chr>                     <chr>   <chr>         <chr>        
    ##  1 1/27/2022 12:38 Mission Foodhall          3100 1… 1/26/2022     Specialty Fo…
    ##  2 1/27/2022 12:41 Fred’s Liquors & Delicat… 200 Va… 1/26/2022     Grocery Store
    ##  3 1/27/2022 12:43 E And M Market            399 Va… 1/26/2022     Convenience …
    ##  4 1/27/2022 12:46 K & H Liquor              501 Va… 1/26/2022     Convenience …
    ##  5 1/27/2022 12:48 Valencia Whole Foods      999 Va… 1/26/2022     Grocery Store
    ##  6 1/27/2022 12:50 Decamere Market           1001 V… 1/26/2022     Convenience …
    ##  7 1/27/2022 12:52 Indian Spices and Grocery 3265 2… 1/26/2022     Specialty Fo…
    ##  8 1/27/2022 12:55 Valencia Farmer’s Market  1299 V… 1/26/2022     Grocery Store
    ##  9 1/27/2022 12:59 Valencia Grocery          1300 V… 1/26/2022     Convenience …
    ## 10 1/27/2022 13:02 Mr. Liquor                1200 V… 1/26/2022     Convenience …
    ## # … with 84 more rows, and 47 more variables:
    ## #   What.type.of.Specialty.Food.Store. <chr>, EBT.Accepted. <chr>,
    ## #   Number.of.Locations..chain.. <dbl>, Median.Price.of.a.Dozen.Eggs <dbl>,
    ## #   Median.Price.of.a.Loaf.of.Bread <dbl>,
    ## #   Median.Price.of.a.Gallon.of.Milk <chr>, Milk.Standardized_Gallon <dbl>,
    ## #   Median.Price.of.Oranges <chr>, Orange.Standardized_lbs <dbl>,
    ## #   Median.Price.of.Organic.Oranges <chr>, …

``` r
plot(just_geo, graticule = st_crs(4326), key.pos = 1)
plot(intersection[1], col = "black", pch = 19, add = TRUE)
```

![](Honors-Thesis-Workbook_files/figure-gfm/unnamed-chunk-31-1.png)<!-- -->

``` r
#ethnicity
just_geo_2 <- mission_percents_clean
just_geo_2 <- st_set_crs(just_geo_2, "WGS84")
```

    ## Warning: st_crs<- : replacing crs does not reproject data; use st_transform for
    ## that

``` r
intersection_2 <- st_intersection(x = just_mission_stores, y = just_geo_2)
```

    ## Warning: attribute variables are assumed to be spatially constant throughout all
    ## geometries

``` r
plot(just_geo_2$geometry, graticule = st_crs(4326), key.pos = 1)
```

    ## Warning in title(...): "key.pos" is not a graphical parameter

``` r
plot(intersection_2[1], col = "black", pch = 19, add = TRUE)
```

![](Honors-Thesis-Workbook_files/figure-gfm/unnamed-chunk-32-1.png)<!-- -->

``` r
# Number of Retailers in each Median Income Group
int_result <- intersection_join %>% 
  group_by(median_income) %>% 
  count()

as.data.frame(int_result)
```

    ## # A tibble: 4 × 3
    ##   median_income         n                                                   geom
    ##   <chr>             <int>                                       <MULTIPOINT [°]>
    ## 1 110,001 - 145,000    31 ((-122.4162 37.76762), (-122.4138 37.77127), (-122.41…
    ## 2 145,001 - 180,000     8 ((-122.4247 37.76133), (-122.4236 37.76176), (-122.42…
    ## 3 40,000 - 75,000      12 ((-122.4213 37.77306), (-122.4194 37.76815), (-122.42…
    ## 4 75,001 - 110,000     43 ((-122.4227 37.77174), (-122.4243 37.77088), (-122.42…

``` r
#EBT Test
EBT_result <- intersection_join %>% 
  group_by(median_income, EBT.Accepted.) %>% 
  count()

as.data.frame(EBT_result)
```

    ## # A tibble: 8 × 4
    ##   median_income     EBT.Accepted.     n                                     geom
    ##   <chr>             <chr>         <int>                         <MULTIPOINT [°]>
    ## 1 110,001 - 145,000 No               15 ((-122.4138 37.77127), (-122.4163 37.77…
    ## 2 110,001 - 145,000 Yes              16 ((-122.4162 37.76762), (-122.4153 37.76…
    ## 3 145,001 - 180,000 No                5 ((-122.4216 37.75994), (-122.4239 37.76…
    ## 4 145,001 - 180,000 Yes               3 ((-122.4247 37.76133), (-122.4236 37.76…
    ## 5 40,000 - 75,000   No                4 ((-122.4217 37.76475), (-122.4209 37.76…
    ## 6 40,000 - 75,000   Yes               8 ((-122.4213 37.77306), (-122.4194 37.76…
    ## 7 75,001 - 110,000  No               15 ((-122.4243 37.77088), (-122.4226 37.76…
    ## 8 75,001 - 110,000  Yes              28 ((-122.4227 37.77174), (-122.4246 37.76…

# Results (lens of Agency)

``` r
contruct_tab <- intersection_2 %>%
  select(Majority, geometry)
primary_table <- st_join(intersection_join, contruct_tab)
primary_table
```

    ## # A tibble: 94 × 53
    ##    Timestamp       Name.of.Food.Retailer     Address Date.Assessed Type.of.Store
    ##    <chr>           <chr>                     <chr>   <chr>         <chr>        
    ##  1 1/27/2022 12:38 Mission Foodhall          3100 1… 1/26/2022     Specialty Fo…
    ##  2 1/27/2022 12:41 Fred’s Liquors & Delicat… 200 Va… 1/26/2022     Grocery Store
    ##  3 1/27/2022 12:43 E And M Market            399 Va… 1/26/2022     Convenience …
    ##  4 1/27/2022 12:46 K & H Liquor              501 Va… 1/26/2022     Convenience …
    ##  5 1/27/2022 12:48 Valencia Whole Foods      999 Va… 1/26/2022     Grocery Store
    ##  6 1/27/2022 12:50 Decamere Market           1001 V… 1/26/2022     Convenience …
    ##  7 1/27/2022 12:52 Indian Spices and Grocery 3265 2… 1/26/2022     Specialty Fo…
    ##  8 1/27/2022 12:55 Valencia Farmer’s Market  1299 V… 1/26/2022     Grocery Store
    ##  9 1/27/2022 12:59 Valencia Grocery          1300 V… 1/26/2022     Convenience …
    ## 10 1/27/2022 13:02 Mr. Liquor                1200 V… 1/26/2022     Convenience …
    ## # … with 84 more rows, and 48 more variables:
    ## #   What.type.of.Specialty.Food.Store. <chr>, EBT.Accepted. <chr>,
    ## #   Number.of.Locations..chain.. <dbl>, Median.Price.of.a.Dozen.Eggs <dbl>,
    ## #   Median.Price.of.a.Loaf.of.Bread <dbl>,
    ## #   Median.Price.of.a.Gallon.of.Milk <chr>, Milk.Standardized_Gallon <dbl>,
    ## #   Median.Price.of.Oranges <chr>, Orange.Standardized_lbs <dbl>,
    ## #   Median.Price.of.Organic.Oranges <chr>, …

\##Access \###Geography \####map

``` r
tmap_mode("plot")
```

    ## tmap mode set to plotting

``` r
income_map_with_retail
```

![](Honors-Thesis-Workbook_files/figure-gfm/unnamed-chunk-36-1.png)<!-- -->

``` r
ethnicity_with_retail
```

![](Honors-Thesis-Workbook_files/figure-gfm/unnamed-chunk-36-2.png)<!-- -->
\####tables

``` r
median_count <- intersection_join %>% 
  group_by(median_income) %>% 
  count() %>%
  rename("number of retailers" = "n")
median_count
```

    ## # A tibble: 4 × 3
    ##   median_income     `number of retailers`                                   geom
    ##   <chr>                             <int>                       <MULTIPOINT [°]>
    ## 1 110,001 - 145,000                    31 ((-122.4162 37.76762), (-122.4138 37.…
    ## 2 145,001 - 180,000                     8 ((-122.4247 37.76133), (-122.4236 37.…
    ## 3 40,000 - 75,000                      12 ((-122.4213 37.77306), (-122.4194 37.…
    ## 4 75,001 - 110,000                     43 ((-122.4227 37.77174), (-122.4243 37.…

``` r
#as.data.frame(int_result)

ethnicity_count <- intersection_2 %>%
  group_by(Majority) %>%
  count() %>%
  rename("number of retailers" = "n")
ethnicity_count
```

    ## # A tibble: 2 × 3
    ##   Majority           `number of retailers`                              geometry
    ##   <chr>                              <int>                      <MULTIPOINT [°]>
    ## 1 Hispanic or Latinx                    52 ((-122.4217 37.76475), (-122.4194 37…
    ## 2 White                                 42 ((-122.4213 37.77306), (-122.4227 37…

``` r
#as.data.frame()
```

\####Price

``` r
price_table <- primary_table %>%
  mutate(egg_quartile = cut(primary_table$Median.Price.of.a.Dozen.Eggs, quantile(primary_table$Median.Price.of.a.Dozen.Eggs, na.rm = TRUE),include.lowest=TRUE,labels=FALSE)) %>%
  select(-Timestamp, -Address, -Date.Assessed, -Type.of.Store, -What.type.of.Specialty.Food.Store., -EBT.Accepted., -Number.of.Locations..chain.., -Is.there.signage.in.other.languages.than.English., -If.so..what.languages., -Access.Notes, -Is.there.fresh.produce.available., -What.percentage.of.the.store.is.produce., -Is.there.organic.produce.available., -Is.there.local.produce.available., -How.many.types.of.fresh.produce.are.available., -Is.there.an.ethnic.section., -Are.there.options.besides.national.name.brand.ethnic.foods.,, -What.ethnic.food.nationalities.are.available., -Selection.Notes, -Is.there.signage.or.visible.documentation.of.environmental.work.or.actions., -If.so..what.kind.of.environmental.work., -Is.there.signage.or.visible.documentation.of.social.justice.work.or.actions., -If.so..what.kind.of.social.justice.work., -General.Notes, -address) %>%
  mutate(bread_quartile = cut(primary_table$Median.Price.of.a.Loaf.of.Bread, quantile(primary_table$Median.Price.of.a.Loaf.of.Bread, na.rm = TRUE),include.lowest=TRUE,labels=FALSE)) %>%
  mutate(milk_quartile = cut(primary_table$Milk.Standardized_Gallon, quantile(primary_table$Milk.Standardized_Gallon, na.rm = TRUE),include.lowest=TRUE,labels=FALSE)) %>%
  mutate(orange_quartile = cut(primary_table$Orange.Standardized_lbs, quantile(primary_table$Orange.Standardized_lbs, na.rm = TRUE),include.lowest=TRUE,labels=FALSE))
price_table
```

    ## # A tibble: 94 × 32
    ##    Name.of.Food.Retailer      Median.Price.of… Median.Price.of… Median.Price.of…
    ##    <chr>                                 <dbl>            <dbl> <chr>           
    ##  1 Mission Foodhall                       7.49             9.99 5.49 (half)     
    ##  2 Fred’s Liquors & Delicate…             6.99             5.69 7.49            
    ##  3 E And M Market                         4.99             5.99 5.69            
    ##  4 K & H Liquor                          NA               NA    3.50 (half)     
    ##  5 Valencia Whole Foods                   5.99             5.49 8.99            
    ##  6 Decamere Market                       NA               NA    2.59 (half)     
    ##  7 Indian Spices and Grocery             NA               NA    <NA>            
    ##  8 Valencia Farmer’s Market               4.74             4.69 5.99            
    ##  9 Valencia Grocery                       3.99            NA    3.99            
    ## 10 Mr. Liquor                            NA               NA    <NA>            
    ## # … with 84 more rows, and 28 more variables: Milk.Standardized_Gallon <dbl>,
    ## #   Median.Price.of.Oranges <chr>, Orange.Standardized_lbs <dbl>,
    ## #   Median.Price.of.Organic.Oranges <chr>,
    ## #   Organic.Oranges.Standardized_lbs <dbl>, Median.Price.of.Avocados <chr>,
    ## #   Standardized.Avocado_each <dbl>, Median.Price.of.Organic.Avocados <chr>,
    ## #   Standardized.Organic.Avocado_each <dbl>, Median.Price.of.Carrots <chr>,
    ## #   Standardized.Carrots_lbs <dbl>, Median.Price.of.Organic.Carrots <chr>, …

\##Health & Nutrition

\##Cultural Relevance

\##Sustainability
