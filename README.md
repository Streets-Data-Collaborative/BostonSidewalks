# BostonSidewalks

Profiling the sidewalks of Boston from a social distancing point of view.

**Sidewalk Stress Index**

To develop the sidewalk stress index, we considered two criteria:

* Population Density:
Obtained from the [LandScan datasource](https://hifld-geoplatform.opendata.arcgis.com/datasets/landscan-usa). Provides day and night incident population for a given area. It is a raster dataset with a pixel of approximately 90m by 90m size.

* Sidewalk Width: 
Obtained from the [Analyze Boston](https://data.boston.gov/dataset/sidewalk-inventory) which is the City of Boston's open data hub. It includes data on sidewalk segments in the City of Boston. The main variable we are interested in is the Sidewalk Width, which is in feet.

By converting the raster population data into polygons, the mean sidewalk width incident on the cell was calculated with a spatial join. 

```{r}

library(sf)
library(dplyr)

# Normalizing data to export as a shp file

ls_day_boston <- read_sf("landscan_r_analysis/boston_day_stress/boston_day_stress.shp")
ls_ngt_boston <- read_sf("landscan_r_analysis/boston_night_stress/boston_night_stress.shp")

# Calculating percentile rank to get normalized data:

# daytime population:
ls_day_boston$nrm_pop_dy <- percent_rank(ls_day_boston$gridcode)
ls_day_boston$nrm_swk_dy <- percent_rank(ls_day_boston$SWK_WIDTH)
ls_day_boston$stress_dy <- ls_day_boston$nrm_pop_dy-ls_day_boston$nrm_swk_dy

#nighttime population
ls_ngt_boston$nrm_pop_nt <- percent_rank(ls_ngt_boston$gridcode)
ls_ngt_boston$nrm_swk_nt <- percent_rank(ls_ngt_boston$SWK_WIDTH)
ls_ngt_boston$stress_nt <- ls_ngt_boston$nrm_pop_nt-ls_ngt_boston$nrm_swk_nt

# saving shapefiles
st_write(ls_day_boston, "landscan_r_analysis/boston_day_stress/boston_day_stress.shp", delete_layer = TRUE)
st_write(ls_ngt_boston, "landscan_r_analysis/boston_night_stress/boston_night_stress.shp", delete_layer = TRUE)

```

Both values were normalized by percentile ranking between 0 & 1. By subtracting each cell's normalized population, with its corresponding normalized mean sidewalk width, we could compare (city-wide) how high or low the ratio was compared to the city-wide average. A negative score indicates lower than average stress, and a positive score indicates higher than average stress. Thus, we can consider **four** situational extremes:

**Positive Score:** 0.01 to +1
* Low Density & High Sidewalk width
* High Density & Low Sidewalk width

**Negative Score:** -1 to -0.01
* Low Density & Low Sidewalk width
* High Density & High  Sidewalk width

**Neutral Score:**
* The fifth situation, would be a score of 0, indicating said location has a stress score comparable to the city-wide average.

![RELATIONSHIP_MAP](https://user-images.githubusercontent.com/39370828/87182895-0a8a6d00-c2b3-11ea-92f7-e8b4d6943879.jpg)

Sidewalks – Are they good enough?

Social distancing norms in the wake of the Covid-19 outbreak suggest keeping a distance of at least 6 feet from another person when outdoors. 

Can we say something about where physical distancing by looking at Boston's sidewalks?
Can we estimate which areas are more likely to conform to distancing guidelines based on combining sidewalk and other data?
 
To ensure that residents are able to comply with social distancing guidelines Many cities have restricted vehicular traffic on certain streets, or extended ‘sidewalks’ by taking in lanes by adding flex posts or traffic cones.




**Data**
1. Polyline and polygon shapefiles of sidewalks for the city of Boston. These can be used to identify sections of sidewalks and streets which do not adequately serve width regulations. 

2. [LandScan data](https://www.ornl.gov/news/gis-landscan-goes-public) - Widely considered the "gold standard of population and mapping data in the United States, (this dataset) captures daytime and nighttime activity of the U.S. population at a resolution of roughly 90 meters or about 300 feet."

**Analysis**

1. Profile Boston Sidewalks for completeness and quality
2. Join with Landscan data
3. Identify areas with high/low sidewalk<>human activity
4. [Build a relationship map](https://www.esri.com/arcgis-blog/products/arcgis-online/mapping/what-is-a-relationship-map/)
5. Identify areas that are likely to be infection hotspots (high population activity, low sidewalk widths)

## Future directions - Identifying 15-minute accessible regions**

Paris, under their mayor Anne Hidalgo is working to completely transform how people move around their city by introducing [the ’15-minute’ city](https://www.citylab.com/environment/2020/02/paris-election-anne-hidalgo-city-planning-walks-stores-parks/606325/), where all aspects of a person’s life are achievable within a 15-minute walk, bike, or transit ride from their residence.

A project of this scale and magnitude will be required to be staged and completed in phases. If we consider the city of Boston, Massachusetts, how can we adapt this ’15-minute’ city plan here, taking into account its unique strengths, weaknesses, opportunities, and challenges? 

**Analysis**

* Can we use POI data to evaluate the accessibility of various 15-minute regions based on population and car ownership? 
* [Can we create accessibility maps](https://towardsdatascience.com/measuring-pedestrian-accessibility-97900f9e4d56) that allow Paris and other cities identify which areas require more amenities to make it eligible under a 15-minute accessible region?

**Narrative**
* Who and where will interventions make the most difference? 
* How can we avoid falling into the systematic bias created by 20 th century urban planning?
* How can we create a general purpose analysis to evaluate 15-minute accessibility for any city?
