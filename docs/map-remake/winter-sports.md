---
tags:
  - QGIS
  - OSGeo
  - FOSS4G
  - OpenStreetMap
  - Dati vettoriali
---
# The Winter Catch: Mapping Italy’s 1-Hour Alpine Reach

Whenever we see an infographic about the **Milano-Cortina 2026 Olympics**, we see maps, a lot of maps. In these days of Olympic enthusiasm, an article from *The Washington Post* may have attracted the interest of chartography enthusiasts. [*"Explore where Winter Olympic sports are most accessible across the U.S."*](https://www.washingtonpost.com/sports/olympics/interactive/2026/winter-olympic-sports-city-accessibility/), with maps by Dylan Moriarty and Kati Perry and reporting by Emily Giambalvo, explores the accessibility of winter sports facilities across the USA to understand the real impact of these sports, which we only see at elite level every four years.

In this post, we reverse-engineer a classic "**catchment analysis**." We aren't just looking at where the rinks and slopes are, but we are asking: *How many Italians can actually reach them in an hour?* and we try to find answers using QGIS and available open data on facilities location and population distribution.

## Learning Objectives

- **Network Analysis**: Generate drive-time isochrones with the ORS plugin.

- **Data Integration**: Handle both Vector (from OpenStreetMap) and Raster (from WorldPop) datasets.

- **Spatial Statistics**: Use Zonal Statistics to aggregate population counts.

- **Comparative Analytics**: Evaluate the "diversity" of sports across different regions.

## The Toolkit: Data & Plugins

| Data/Plugin|Source|Purpose|
|---|---|---|
|ORS Tools Plugin|QGIS Plugin Manager|Calculates driving-time isochrones.|
|Winter Sports facilities|OpenStreetMap (Overpass)|Locations of hockey, skating, bobsleigh, etc.|
|Population Raster|WorldPop.org|100m resolution population density for Italy (ref.2020).|
|Administrative Borders|ISTAT|To define the national study area.|

## Step-by-Step Workflow

### 1. Gathering the "Ice and Snow" Data

We will extract all winter sports facilities from OpenStreetMap. In QGIS, use the QuickOSM plugin with the following OSM Key/Value pairs:

|Key | Value | WikiOSM | Geometry |
|---|---|---|---|
|sport|bobsleigh|[Doc](https://wiki.openstreetmap.org/wiki/Tag:sport%3Dbobsleigh)| Node, Way, Closed Way|
|sport|curling|[Doc](https://wiki.openstreetmap.org/wiki/Tag:sport%3Dcurling)| Node, Closed Way|
|sport|hockey|[Doc](https://wiki.openstreetmap.org/wiki/Tag:sport%3Dice_hockey)| Node, Closed Way|
|sport|ice_skating|[Doc](https://wiki.openstreetmap.org/wiki/Tag:sport%3Dice_skating)| Node, Closed Way|
|sport|ski_jumping|[Doc](https://wiki.openstreetmap.org/wiki/Tag:sport%3Dski_jumping)| Node, Way, Closed Way|
|sport|biathlon|[Doc](https://wiki.openstreetmap.org/wiki/Tag:sport%3Dbiathlon)| Node, Way, Closed Way|
|piste:type|nordic|[Doc](https://wiki.openstreetmap.org/wiki/Tag:piste:type%3Dnordic)| Way, Closed Way|
|piste:type|downhill|[Doc](https://wiki.openstreetmap.org/wiki/Tag:piste:type%3Ddownhill)| Way, Closed Way|

...  or run a query in [Overpass Turbo](https://overpass-turbo.eu/s/2kOG). Here's an example for downhill facilities:

```
/* Extracting downhill ski facilities in Italy */
[out:json][timeout:2500];
// fetch area “Italy” to search in
{{geocodeArea:Italy}}->.searchArea;
// gather results
nwr["piste:type"~"downhill"](area.searchArea);
// print results
out geom;
```

> **Tip**: For linear features like cross-country skiing tracks, use *Vector > Geometry Tools > Extract Specific Vertices* (Index 0 and -1) to identify the entry points (gateways) of the tracks. For polygonal features, use *Vector geometry > Centroids*. Hence, copy and paste newly created points geometry inside the Overpass-derived point geometry layer of the corresponding sport type.

### 2. The 60-Minute Radius (Isochrones)

- Open *ORS Tools > Isochrones > Isochrones from Point-Layer*

- Input: Your points (hockey rinks, ski gateways, etc.).

- Travel Mode: driving-car

- Dimension: time

- Comma-separated ranges: 60 (minutes)

- Location type: destination

### 3. Preparing the population data

Download the [WorldPop Italy 2020 raster](https://hub.worldpop.org/doi/10.5258/SOTON/WP00645). Each pixel represents the number of people living in that 100m x 100m area. Ensure your project is set to EPSG:32632 (UTM 32N) to ensure that area-based calculations remain accurate. Project the layer accordingly.

### 4. Spatial analysis

This is where we turn geometry into meaningful insight.

#### Calculate the national population

To know the percentage of people reached, we need the total population of Italy as seen by our raster.

- Tool: *Processing Toolbox > Raster Layer Statistics*.

> Note: Look for the SUM value in the HTML output. (Let's assume PopTotal​≈59,000,000).

#### Zonal statistics

We want to "sum" every person (pixel) inside our isochrones.

- Run *Processing Toolbox > Zonal Statistics*

- Input layer: isochrones calculated in the previous step.

- Raster layer: WorldPop raster.

- Output column prefix: pop_

- Statistics to calculate: Sum

Your attribute table now shows exactly how many people live within an hour of each facility.

### 5. Defining accessibility indexes

Open the *Field Calculator* in the *Attribute Table* of the isochrones to create our performance indicators:

- **National Coverage (%)**

How much of Italy is "served"?

Expression: *"pop_sum" / 59000000 * 100*

- **Population Density (People/km²)**

To understand if the rink is in a high-density urban area or a low-density mountain area:

Expression: *"pop_sum" / ($area / 1000000)*

[UNDER CONSTRUCTION]

### 6. Comparison with 2026 Italian athletes hometown

Query WikiData

```
SELECT ?athlete ?athleteLabel (GROUP_CONCAT(DISTINCT ?eventLabel; separator=", ") AS ?events)
WHERE {
  {
    SELECT DISTINCT ?athlete ?event WHERE {
      # 1. Start with the most restrictive filter: Italian Citizens
      ?athlete wdt:P27 wd:Q38 .
      
      # 2. Check for the specific Occupation (Olympic athlete)
      ?athlete wdt:P106/wdt:P279* wd:Q50995749 .
      
      # 3. Connect to the 2026 Winter Olympics hierarchy
      ?event wdt:P361* wd:Q4630399 .
      { ?event wdt:P710 ?athlete . }
      UNION
      { ?athlete wdt:P1344 ?event . }
    }
  }
  
  # 4. Fetch labels outside the complex logic to prevent timeouts
  SERVICE wikibase:label { 
    bd:serviceParam wikibase:language "[AUTO_LANGUAGE],it,en". 
    ?athlete rdfs:label ?athleteLabel .
    ?event rdfs:label ?eventLabel .
  }
}
GROUP BY ?athlete ?athleteLabel
ORDER BY ?athleteLabel
```

