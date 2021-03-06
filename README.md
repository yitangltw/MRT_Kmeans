# Grouping MRT Stations using K-means Clustering

Use MRT hourly data to run Kmeans analysis based on entrance and exit number of people for each station 
</br>
You can also read the article at [__Medium__](https://medium.com/urban-matters/%E6%8D%B7%E9%81%8B%E5%88%86%E6%99%822-f351661ce609) for reference.

Continue on the project [_MRT_Cleaning_Visualizing_](https://github.com/ShihWen/MRT_Cleaning_Visualizing), here the data will be reshaped and divied into entrance and exit for each station, and run K-means clustering in order to explore deeper relation between stations in terms of people flow.</br>

Below is the process flow:
</br>
![](https://github.com/ShihWen/MRT_Kmeans/blob/master/image/flow_chart.png)
</br>
Steps

1. Refine the data using functions in _MRT_cleaning_visualizing.ipynb_, which will be used as raw data for K-means, </br>where the data for each stations has been transfered from 7*21 table to a list and normalized.
![](https://github.com/ShihWen/MRT_Kmeans/blob/master/image/raw_data.png)
2. Run K-means analysis with those hourly number of people as variables by _MRT_K-means_Analysis.ipynb_, which will generate:
    * k_pack_IN/OUT csv file for raw data of entrance and exit separately
    * cluster_group_IN/OUT csv file showing which stations belong to which cluster group
    * line graph and heat map grouped by cluster
    * df_cluster.csv showing the entrance and exit group for each station
3. _MRT_K-means_Analysis.ipynb_ visualize the result in terms of clusters by heat map and line graph:

|Entrance Cluster 0|Entrance Cluster 1|Entrance Cluster 2|Entrance Cluster 3|
| ------------- |:-------------:| :-----:| :-----:|
| ![](https://github.com/ShihWen/MRT_Kmeans/blob/master/notebook_illustration/All_in_heatmap_0_3.png)|![](https://github.com/ShihWen/MRT_Kmeans/blob/master/notebook_illustration/All_in_heatmap_1_3.png)|![](https://github.com/ShihWen/MRT_Kmeans/blob/master/notebook_illustration/All_in_heatmap_2_3.png)|![](https://github.com/ShihWen/MRT_Kmeans/blob/master/notebook_illustration/All_in_heatmap_3_3.png)|

|Exit Cluster 0|Exit Cluster 1|Exit Cluster 2|Exit Cluster 3|
| ------------- |:-------------:| :-----:| :-----:|
| ![](https://github.com/ShihWen/MRT_Kmeans/blob/master/notebook_illustration/All_out_heatmap_0_3.png)|![](https://github.com/ShihWen/MRT_Kmeans/blob/master/notebook_illustration/All_out_heatmap_1_3.png)|![](https://github.com/ShihWen/MRT_Kmeans/blob/master/notebook_illustration/All_out_heatmap_2_3.png)|![](https://github.com/ShihWen/MRT_Kmeans/blob/master/notebook_illustration/All_out_heatmap_3_3.png)|

Line graph for entance:
![](https://github.com/ShihWen/MRT_Kmeans/blob/master/notebook_illustration/All_in_lineGraph.png)
Line graph for exit:
![](https://github.com/ShihWen/MRT_Kmeans/blob/master/notebook_illustration/All_out_lineGraph.png)

4. Visualize the result in terms of single station via _MRT_K-means_StationDashboard.ipynb_, which generates dashboard for all stations under the folder created by _MRT_K-means_Analysis.ipynb_:
![](https://github.com/ShihWen/MRT_Kmeans/blob/master/notebook_illustration/single_plot/1_2/BL12%20Plot.png)

5. Geo-visualize the result using QGIS and define the clusters by their patters into:
   1. Peak in the morning (cluster 0)
   2. Peak in both morning and afternoon, and weekends (cluster 1)
   3. Peak in the afternoon (cluster 2)
   4. Peak in both morning and afternoon (cluster 3)

|Entrance Cluster 0|Entrance Cluster 1|
| :-------------: |:-------------:|
| Peak in the morning |Peak in both morning and afternoon, and weekends|
| ![](https://github.com/ShihWen/MRT_Kmeans/blob/master/image/inward_3.png)|![](https://github.com/ShihWen/MRT_Kmeans/blob/master/image/inward_1.png)|

|Entrance Cluster 2|Entrance Cluster 3|
| :-------------: |:-------------:|
| Peak in the afternoon |Peak in both morning and afternoon|
| ![](https://github.com/ShihWen/MRT_Kmeans/blob/master/image/inward_4.png)|![](https://github.com/ShihWen/MRT_Kmeans/blob/master/image/inward_2.png)|

6. For each station, merge its entrance and exit cluster in to final category.
There are 16 possible combinations but only 9 generated in practice:
![](https://github.com/ShihWen/MRT_Kmeans/blob/master/image/final_table.jpeg)


Below shows the distrubution of stations in group A, B and D:</br>
It is significant to notice the stations regard as residential group are distributed around Taipei City, while work place and leisure tpyes are located at the center of the city.

|Group A|Group B|Group D|
| :-------------: |:-------------:| :-----:|
|Entrance: Peak at a.m.</br>Exit: Peak at p.m. |Entrance: Peak at p.m.</br>Exit: Peak at a.m.|Entrance: Peak at Both + Weekend</br>Exit: Peak at both + weekend|
|Type: Residential|Type: Work Place|Type: Residential, Work and Leisure|
| ![](https://github.com/ShihWen/MRT_Kmeans/blob/master/image/final_a.png)|![](https://github.com/ShihWen/MRT_Kmeans/blob/master/image/final_b.png)|![](https://github.com/ShihWen/MRT_Kmeans/blob/master/image/final_d.png)|
