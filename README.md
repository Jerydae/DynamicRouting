# DynamicRouting
Grouping stores near the nearest warehouse in the region.

# Shop Location Clustering and Visualization Project
This project demonstrates how to cluster shop locations using K-Means clustering and visualize these clusters on a map with Convex Hull boundaries. The project also overlays a basemap for better spatial context.

## Table of Contents

[Project Overview](#project-overview)

[Data](#data)

[Dependencies](#dependencies)

[Code Overview](#code-overview)

[Running the Project](#running-the-project)

[Results](#results)

[Future Improvements](future-improvements)

### Project Overview

This project focuses on analyzing the geographic distribution of shops and warehouses. By clustering the shops based on their locations and visualizing these clusters with Convex Hull boundaries, we can gain insights into the spatial distribution and proximity of shops to warehouses.

### Data

Shops Dataset: Contains the latitude and longitude of shops (`duka_latitude`, `duka_longitude`).

Warehouses Dataset: Contains the latitude and longitude of warehouse centroids (`warehouse_latitude`, `warehouse_longitude`).

### Dependencies

To run this project, you will need the following Python libraries:

`pip install geopandas contextily matplotlib scipy scikit-learn numpy pandas`


### Code Overview

The key steps in the code include:

Loading Data: The project starts by loading shop and warehouse data from CSV files.

Clustering: K-Means clustering is applied to group shops based on their proximity to predefined warehouse centroids.

Geospatial Data Preparation: GeoPandas is used to convert the data into a geospatial format and reproject it for visualization.

Visualization: The clusters and Convex Hull boundaries are plotted on a basemap using Matplotlib and Contextily.

### Code Snippet

## Loading the datasets

`shops = pd.read_csv('dataset.csv')`

`warehouses = pd.read_csv('territories_centroids.csv')`

## Prepare data for clustering

`shop_locations = shops[['duka_latitude', 'duka_longitude']]`

## Using K-Means clustering

`kmeans = KMeans(n_clusters=len(warehouses), init=warehouses[['warehouse_latitude', 'warehouse_longitude']].values, n_init=1)`

`shops['cluster'] = kmeans.fit_predict(shop_locations)`

## Convert to GeoDataFrames

`shops_gdf = gpd.GeoDataFrame(shops, geometry=gpd.points_from_xy(shops['duka_longitude'], shops['duka_latitude']), crs='EPSG:4326')`

`warehouses_gdf = gpd.GeoDataFrame(warehouses, geometry=gpd.points_from_xy(warehouses['warehouse_longitude'], warehouses['warehouse_latitude']), crs='EPSG:4326')`

## Reproject for basemap

`shops_gdf = shops_gdf.to_crs(epsg=3857)`

`warehouses_gdf = warehouses_gdf.to_crs(epsg=3857)`

## Running the Project

1. Clone the repository
   `git clone https://github.com/Habiba-Hussein/Dynamic-Routing.git`
   `cd your-repo-name`

2. Install the required dependencies
3. Run the Python script

## Results
The output of the project is a map displaying the clustered shop locations, warehouse locations, and the Convex Hull boundaries for each cluster.

![image](https://github.com/user-attachments/assets/8b09578c-cb5c-4815-b179-d7c468273d42)


## Future Improvements

- Implement more advanced clustering techniques
- Expand the dataset to include more geographical regions

