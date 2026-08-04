Adelaide Mobility Gaps: Spatial Equity and Accessbility Analysis of Greater Adelaides Public Transit Network

Core Questions:
1) What percentage of residents reside in each suburb are within a 10 minute walk (800m) or a 15 minute feeder bus to high frequency transit hubs on a given work/weekday?
2) Which regions have high car dependency or low household vehicle ownership, combined with low transit access scores?
3) Where are the optimal locations to introduce micro mobility hubs (e-bikes) or high frequency feeder bus routes to bridge this gap?


To answer these:
1) Public Transport Schedules and Network Features:
    - Sourced from Data.SA
        - stops.txt (all stops for buses, trains and trams)
        - routes.txt and trips.txt (identifies higher frequency stops with more frequency)
        - calendar.txt (isolate a regular workday)

2) Demographics and Spatial Barriers:
    - Sourced from ABS Census 2021 data
        - Number of motor vehicles per household
        - Method of Travel to Work
        - Index of Relative Socio-economic Disadvantage Score
    - Calculate transit dependency index based on low vehicle ownership and lower socio-economic status

3) Road and Pedestrian Network:
    - Sourced from OpenStreetMap via OSMnx in Python or Location SA transport layer
    - Build walkable/drivable dataset in ArcGIS Network Analyst
    - Build service Area Isochrones
        - Walking Catchments (5m (400m), 10m (800m), 15m (1200m) walking around hubs)
        - Feeder Bus Catchments (15m travel time for local buses to hubs)
            - Hubs are: 
                - Rail: Adelaide Railway Station, Gawler, Salisbury, Noarlunga
                - Bus: Paradise, Klemzig, Tea Tree Plaza
                - Tram: North Terrace, South Road

4) Spatial Join:
    - Join catchments and ABS demographic polygons
    - Calculate accessability score for each polygon based on:
        - Accessability score (population within 10m walk to frequent transit / total population)
    - Identify mismatched zones, ie. areas with high car dependecy and low car ownership

5) Hotspot Identification:
    - Find under-serviced zones, ie. areas with high commute demand and low transit access

6) Location Optimisation:
    - Use location-allocation tool in arcgis network analyst 
    - set demand points as centroids of under-served locations
    - set candidate locations as major suburban intersections or council owned land
    - solve where to place feeder hubs to maximise population access to 10m travel threshold

7) Visualisation:
    - Interactive web map using ArcGIS Online
    - Before and After visualisation pictures

Tech Stack:
    - ArcGIS Pro Tools: Network Analyst, Spatial Statistics
    - Python Libraries: arcgis, arcpy, geopandas, scikit-learn, osmnsx, pandas
    - Data Sources: Data.SA (GTFS), ABS Census Data, OpenStreetMap  
