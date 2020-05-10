# BostonSidewalks
Profiling the sidewalks of Boston

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

**Future directions - Identifying 15-minute accessible regions**

Paris, under their mayor Anne Hidalgo is working to completely transform how people move around their city by introducing [the ’15-minute’ city](https://www.citylab.com/environment/2020/02/paris-election-anne-hidalgo-city-planning-walks-stores-parks/606325/), where all aspects of a person’s life are achievable within a 15-minute walk, bike, or transit ride from their residence.

A project of this scale and magnitude will be required to be staged and completed in phases. If we consider the city of Boston, Massachusetts, how can we adapt this ’15-minute’ city plan here, taking into account its unique strengths, weaknesses, opportunities, and challenges? 

**Analysis**

* Can we use POI data to evaluate the accessibility of various 15-minute regions based on population and car ownership? 
* [Can we create accessibility maps](https://towardsdatascience.com/measuring-pedestrian-accessibility-97900f9e4d56) that allow Paris and other cities identify which areas require more amenities to make it eligible under a 15-minute accessible region?

**Narrative**
* Who and where will interventions make the most difference? 
* How can we avoid falling into the systematic bias created by 20 th century urban planning?
* How can we create a general purpose analysis to evaluate 15-minute accessibility for any city?
