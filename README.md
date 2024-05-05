# Mapping-urban-thermal-environment-and-EV-activity
Spring 2024 | UC Berkeley

1. Introduction
1.1 Background
Extreme heat is the number-one climate killer in the U.S., accounting for more deaths than sea level rise, flooding, drought, and other impacts. Reducing CO2 emissions is a growing challenge for the transport sector. Transportation produces roughly 23 percent of the global CO2 emissions from fuel combustion.  Our primary concern is how can we boost EV usage and equality to boost sustainable urban development towards climate change. We are interested in how the different regions of a city can vary according to different urban environments in Climate Change (LST & CO2). Points of interest (POI) can be Land Surface Temperature (LST) and Carbon dioxide (CO2). A city can have different building types, population density, race density, green space density, and so forth. For now, we selected the following metrics to measure the relationship between POIs like LST, Urban EV CO2 Emission, and Urban Structure.

1.2 Topic Identification
To address these disparities and promote a sustainable city, I'm interested in several metrics that might serve as indicators interacting with climate change and EVs.  So this study aims to use the exploratory data analysis (EDA) method to explore the relationship among selected variables. The primary concern is how to boost EV usage and equality to boost sustainable urban development towards climate change. We are interested in how the different regions of a city can vary according to different urban environments in Climate Change. Points of interest (POI) can be Land Surface Temperature (LST) and Carbon dioxide (CO2). A city can have different building types, population density, race density, green space density, and so forth. For now, we selected the following metrics to measure the relationship between POIs like LST & Urban EV CO2: 
Land Surface Temperature
Electric Vehicle Station Density
Electric Vehicle Demand Density
CO2 Emission Distribution from Electric Vehicles
Green Space Density (Location-based)
Urban Street Typology Structure (Network Centrality, street density, building height, etc)
Race Density

2. Literature Review 
The combined effect of climate change and the urban heat island challenges the living conditions in cities, with consequences on human health, the economy and ecosystems (Revi et al., 2014). The UHI intensity is strongly related both to external influences (e.g., climate, weather, and season) and to the intrinsic characteristics of a city (e.g., city size, building density, and land-use distribution) (Oke 1982). Several papers use linear regression analysis to study the relationship between different Urban Heat Island (UHI) indicators. Typically, these methods are used to develop composite indicators that quantify access by combining a number of individual indicators. Lin et al. (2017) investigate the impact of pocket parks on UHI intensity and Floor Area Ratio (FAR), building density, and Tree Cover Ratio (TCR) as urban planning indicators can significantly decrease UHI. Kammuang-Lue et al. 2015 focused on how population density, building density, and traffic density influence UHII during different seasons. Husni et al. 2022 improved the UHI model for predicting how traffic congestion contributes to the UHI effect. Yin et al. 2018  emphasized that urban form metrics, especially building density,  are critical for UHI mitigation efforts using spatial regression. Lu et al. 2012 utilized regression Analysis of the Relationship between four canopy characteristics: impermeable rate (IR), building density (BD), water body percentage (WBP), and planting rate (PR) with UHI.

Recently, with the implementation of policies related to carbon emission reduction goals, cities have been asked to take an active role in mitigating their contribution to global warming and associated climate change by reducing their CO2 emissions (Hsu et al., 2020). Such policies are motivated by the long-recognized environmental benefits of EVs (Hardman et al., 2017) which include their positive impact on air quality (Liang et al., 2019) and CO2 emissions (Wolfram and Lutsey, 2016). Mussetti et al. (2022) indicated that the full fleet electrification (FE) produces a reduction in near-surface air temperature, and is substantial during the morning traffic peak (up to 0.6°C). Therefore, the adoption of electric vehicles is expected to lead to a decrease in the emission of heat from vehicle exhausts within city settings, enhancing the thermal comfort and environmental quality of urban areas.

3. Data Collection
The data utilized for this mapping analysis combines census-level social demographic data, electrical vehicle trip origin-destination (OD) trajectory data, Google Earth engine urban land surface temperature data, and open street network data. The EV data is connected to geospatial data relating to open street map points of interest. All data was collected online. The  sources of data include:
New York City census county boundary shapefile data (NYC Open Data - (cityofnewyork.us))
Replica EVs trip OD trajectory data (https://www.replicahq.com/)
Bay Area Counties shapefile data: Bay Area Counties | DataSF | City and County of San Francisco (sfgov.org)
MOD11A1.061 Terra Land Surface Temperature and Emissivity Daily Global 1km data (LP DAAC - MOD11A1 (usgs.gov))
U.S. Department of Energy's Alternative Fuels Data Center Electric Vehicle Charging Station (Alternative Fuels Data Center: Maps and Data (energy.gov))
New York State boundary shapefile data 
(Index of /geo/tiger/GENZ2016 (census.gov))
New York City census tract and block group shapefile data 
(Understanding Geographic Identifiers (GEOIDs) (census.gov)
Open Street Map: for data on the locations of green space, and driving roads (https://osmnx.readthedocs.io/en/stable/)

4. Methodology and Result
4.1 Mapping and Measuring Density Distribution Using H3 Hexagonal Hierarchical Geospatial Indexing System
H3 is a geospatial indexing system using a hexagonal grid that can be (approximately) subdivided into finer and finer hexagonal grids, combining the benefits of a hexagonal grid with S2's hierarchical subdivisions. To better understand the mapping results, H3 hexagonal grids were employed in this study to visualize the spatial distribution of urban thermal environment and climate-related electric vehicle (EV) activity. The choice of a hexagonal grid system over traditional square grids was motivated by several key advantages:
Hexagonal cells maintain an equal area across the study region, ensuring that density values are not distorted by varying cell sizes. This property is crucial when mapping thermal and EV activity patterns, as it allows for an accurate representation of the underlying phenomena. 
The hexagonal grid's improved adjacency, with each cell having six equidistant neighbors, facilitates spatial analysis tasks such as interpolation and clustering, enabling more robust modeling of thermal dynamics and EV usage patterns. 
The hexagonal grid mitigates sampling bias associated with square grids, providing more uniform coverage of the study area and reducing the influence of grid orientation on the analysis results. 
The hexagonal grid's visual appeal and ability to create visually appealing patterns and gradients enhance the communication and interpretation of the spatial patterns observed in the urban thermal environment and climate-related EV activity. 
By leveraging the advantages of the hexagonal grid system, this study aimed to provide a comprehensive and accurate representation of the interplay between urban thermal dynamics and EV usage, informing sustainable urban planning and transportation strategies.

4.2 Mapping and Measuring Green Space Data Density Distribution from OpenStreetMap
The locations of leisure parks in New York City were accessed from the OpenStreetMap (OSM) data using the osmnx library. OSM is a collaborative project that provides open-source geographic data, including information on parks and recreational areas. The following methodology was followed to estimate green space (leisure parks) density in New York City for each hexagon:
Filter the green space data
The data was filtered borough-wise to ensure a comprehensive coverage of the study area. Smaller parks with an area of less than 500,000 square meters were excluded from the analysis. This filtering step was performed to focus on larger, more significant green spaces that are likely to have a greater impact on the urban thermal environment and climate-related activities. Smaller parks may not provide sufficient greenery or recreational space to significantly influence these factors.
Define the study area boundary
The boundary of the study area (New York City) was defined using a spatial data file (e.g., a shapefile or GeoJSON) containing the administrative boundaries of the city.
Set the H3 resolution
The desired resolution for the H3 hexagonal grid was set to 8, which determines the size of the hexagonal cells. A higher resolution (larger number) results in smaller hexagon sizes, allowing for a more granular analysis but also increasing computational complexity. The chosen resolution of 8 strikes a balance between spatial detail and computational efficiency for the study area.
Create a GeoDataFrame with H3 hexagons
A GeoDataFrame with H3 hexagons covering the study area was created using the h3.polyfill function from the h3 library. This function generates a set of hexagonal indexes (H3 addresses) that cover the specified geometry (in this case, the New York City boundary). The h3.h3_to_geo_boundary function was then used to convert the H3 addresses to Polygon geometries, which were stored in the GeoDataFrame.
Spatial join between hexagons and parks
A spatial join was performed between the GeoDataFrame containing the H3 hexagons and the leisure parks data. This operation assigns each park to its respective hexagon(s) based on their spatial intersection. The resulting GeoDataFrame contains both the hexagon geometries and the associated park information.
Calculate green space density
For each hexagon, the green space density was calculated by computing the total area of parks within the hexagon and dividing it by the total area of the hexagon. This metric provides a normalized measure of the green space coverage within each hexagonal cell, enabling meaningful comparisons across different areas.
Visualize the green space density distribution
The green space density distribution was visualized using a choropleth map, with the hexagons colored based on their corresponding green space density values. This visualization technique allows for an effective communication of the spatial patterns and variations in green space density across the study area.

4.3 Mapping and Measuring Land Surface Temperature Data Distribution using Google Earth Engine
To analyze the urban thermal environment and its potential impact on climate-related electric vehicle (EV) activity, land surface temperature (LST) data was incorporated into the study. The LST data provides valuable information about the spatial distribution of surface temperatures across the study area, which can influence factors such as urban heat island effects and energy consumption patterns related to EV usage. The LST data was obtained from the Moderate Resolution Imaging Spectroradiometer (MODIS) instrument aboard the Terra and Aqua satellites. Specifically, the MOD11A1 product, which provides daily land surface temperature and emissivity values at a 1-kilometer spatial resolution, was utilized. The data retrieval and processing were facilitated through the Google Earth Engine (GEE) platform, a cloud-based geospatial analysis platform that provides access to a vast repository of remote sensing data and computational resources. The following steps were taken to measure the LST data density distribution using GEE:
Authentication and Initialization
The script authenticated and initialized the GEE Python API, establishing a connection to the GEE environment.
Area of Interest Definition
A rectangular area of interest (AOI) covering New York City was defined using the geographic coordinates -74.2591, 40.4774, -73.7004, 40.9176.
Data Filtering and Processing
The MODIS LST data for daytime temperatures during Spring 2023 was accessed from the GEE data catalog. The data was filtered by date range and the defined AOI and the LST_Day_1km band were selected. The mean LST value across the filtered images was calculated, and the temperature values were converted from Kelvin to Celsius.
Data Clipping and Scaling
The processed LST data was clipped to the bounds of New York City to focus the analysis on the study area. Additionally, the scale of the data was adjusted to reduce the image resolution and size, facilitating more efficient data handling and processing.
Data Download and Alignment
A download URL for the clipped GeoTIFF image was generated, and the data was retrieved using the requests library in Python. The downloaded LST data was then loaded, and its coordinate reference system (CRS) was aligned with the H3 hexagonal grid vector data.
LST Sampling at Hexagon Centroids
For each hexagon in the H3 grid, the centroid was calculated, and the corresponding LST value was sampled from the raster data at the centroid location. This process assigned an LST value to each hexagonal cell, enabling the analysis of the LST density distribution across the study area.
Visualization
The LST raster data and the hexagonal grid with sampled LST values were visualized using appropriate colormaps and choropleth maps, respectively. These visualizations aided in the interpretation and communication of the spatial patterns in the urban thermal environment.
