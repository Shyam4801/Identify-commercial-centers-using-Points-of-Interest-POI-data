# Identify-commercial-centers-using-Points-of-Interest-POI-data
There's a lot of open data available about the demographics and geography of the planet. But this information is not necessarily supervised in any particular structure from which insights can be drawn.

This task is to create clusters of distinct commercial centers or markets using points of interest data of Chennai. Points of interest (POI) data provides location information of different places along with their defining tags like school, type of outlets, type of building, etc.

POI data refers to the coordinates of any physical entity with a tag describing its type like commercial buildings, schools, hospitals, restaurants, etc.

Commercial centres also called Central business district is a city's core business centre which involves a lot of retail , wholesale establishments different from Residential places . But in case of highly dense city like Chennai , there is no clear demarcation of commercial centres , it usually involves an overlap of commercial and residential establishments 
 
Objective:

Get Points of Interest from open data sources like open street maps (OSM).
Understand how spatial location data works
Understand spatial vector data types and how to manipulate it using your language of choice.
Understand necessary GIS concepts like projections, spatial clustering, etc.
Figure out a way of clustering these points into commercial centers/markets. You can use standard size polygons also to cluster the points.
Find and label the most significant clusters, statistically and intuitively. 
Visualize the resultant commercial centres/markets. 

Data Source:

POI (OSM) data- https://www.openstreetmap.org/#map=11/28.6518/77.2219


OSM data are classified into Nodes,Ways,Relations
Nodes are the actual lat long of the point of interest in the map while way is a collection of nodes which may describe a road perhaps ,  boundary of a node or even part of a relation . These data are stored in the form of Point , Linestring , Polygon data in Shapefiles 

Shapefiles store non-topological vector data along with related attribute data
Despite its name indicating a singular file, a shapefile is actually a collection of at least three basic files: .shp, .shx and .dbf.  All three files must be present in the same directory for them to be viewable.  There may be additional files such as a .prj with the shapefile’s projection information. 
shp — Main file : a direct access, variable-record-length file in which each record describes a shape with a list of its vertices.
shx — Index file : In the index file, each record contains the offset of the corresponding main file record from the beginning of the main file. The index file (.shx) contains a 100-byte header followed by 8-byte, fixed-length records.
dbf — dBASE Table file : a constrained form of DBF that contains feature attributes with one record per feature. The one-to-one relationship between geometry and attributes is based on record number. Attribute records in the dBASE file must be in the same order as records in the main file.

METHODOLOGY:

To find the commercial centres we need information about the amenities in the city of Chennai 
We have to cluster these amneties to find segments of the city , K-means is the popular clustering algorithm but K-means is not the ideal data for Coordinates data because it minimizes variances and not the Geodetic distance 

There is considerable amount of distortion with the latitudes that are far away from the equator 
Instead, let’s use an algorithm that works better with arbitrary distances: scikit-learn’s implementation of the DBSCAN algorithm. DBSCAN clusters a spatial data set based on two parameters: a physical distance from each point, and a minimum cluster size. This method works much better for spatial latitude-longitude data.

Having used it we get a couple of clusters with min cluster size set to 2 and epsilon value chosen is 0.05 given the dense nature of the establishments 

DATA VISUALIZATION:

Usual Matplotlib , seaborn are used to visualize clusters , to truly test out our results interactive mapping library called Folium is used to create actual OSM maps which does not involve any API calls hence its faster and more interactive 

WORK IN PROGRESS :

How do we find the significant clusters among these ? 
The method being studied is to use road network to measure the sphere of influence of these amenities 
Popular method called Kernel density estimation is used taking into account the network data to find the significant clusters among these 
