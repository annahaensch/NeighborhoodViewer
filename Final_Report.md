# Neighborhood Analysis of Coffee Shops in Boston, MA

<p align="center">
  <img width="460" height="300" src="https://raw.githubusercontent.com/annahaensch/NeighborhoodViewer/master/Skyline.jpg">
</p>

<p align="center">
Boston skyline viewed from Boston's Back Bay neighborhood.  Image courtesty of <a href = https://www.flickr.com/photos/rjshade/10163674693>Robbie Shade via FlickrCC</a>. 
<p>  




## Introduction

Boston and its many neighborhoods are home to a vibrant selection of bakeries and coffee shops.  Over the years, chain franchises like Dunkin Donuts and Starbucks have gained a strong foothold in the region, as well as many independent teahouses.  Such locales typically serve coffee and tea drinks, as well as light fare and baked goods and cafes.  Some identify as bakeries, others as cafes.  More recently there is an influx of coffee shops serving high-end artisan roasted coffee in a comfortable space conducive to co-working.  Given the large student body, and increasingly remote professional work force in many parts of Boston, such businesses have high potential for success if situated correctly.  

The goal of this data analysis to determine which neighborhood in the Boston/Cambridge, MA region offers the best business opportunity for a new coffee shop,bakery, and co-working space. This will be done by analyzing the existing venues in and around Boston to determine two factors.  First, to determine neighborhoods supporting a large numher of coffee shop and coffee shop type venues.  Second, to determine neighborhoods currently supporting few coffee shops whose overall character of venus is similar to neighborhoods with many coffee shops.  The *target audience* is a group of investors interested in opening a coffee shop.

## Data

Boston/Cambridge and its neighborhoods will be defined by zip codes, neighborhood names, and associated latitude/longitude values.  The neighborhood and zip code data for Boston neighborhoods is obtained by scraping the HTML from a [Boston Globe website](http://archive.boston.com/news/local/articles/2007/04/15/sixfigurezipcodes_city/) and constructing data tables using BeautifulSoup.  Zip code and neighborhood data for Cambridge is obtaied through a [tool built by Randy Majors](https://www.randymajors.com/p/zipcodegmap.html) which uses the Google Maps API. The GIS data for these neighborhoods is obtained through a [repository maintained by GitHub user Eric Hurst](https://gist.githubusercontent.com/erichurst/7882666/raw/5bdc46db47d9515269ab12ed6fb2850377fd869e/US%2520Zip%2520Codes%2520from%25202013%2520Government%2520Data).  Data from the two sources is merged into one pandas dataframe containing all relevent 'Zip_Code,' 'Name,' 'Latitude,' and 'Longitude' values for 34 Boston and Cambridge neighborhoods. 

Data on existing venues in Boston/Cambridge is gathered by querying the Foursquare API, this data is divided into two sets to be analyzed.  First the so-called 'coffee shop adjacent' venues (these are venues in the categories containing the words 'Bakery', 'Coffee', 'Dessert', 'Pastry', 'Café', 'Tea', 'Bagel', 'Donut', or 'Cupcake') are separated and analyzed using matplotlib visualization methods.    Next, a comprehensive analysis of all venues categories is done using kmeans clustering on a dataframe containing neighborhoods with categories ranked by frequency. 

# Methodology

The data was obtained as stated above, and in processing and cleaning, neighborhoods in the same zip code were joined into a single row. From the Foursquare query I obtainted a full list of venues, GIS data, and venue types for each of the neighborhoods.  The first analysis of this data was restricted to venues that are similar to (or might be) coffee shops; I call such venue categories 'coffee shop adjacent.' I built a dataframe one hot encoding all of the coffee shop adjacent venues.  Then I grouped by neighborhood to obtain a dataframe with values counting the total number of each type of coffee shop adjacent venue in each neighborhood. Using this data, I constructed two bar charts using matplotlib.  The first is a stacked horizontal bar chart showing neighborhoods on the y-axis, and total numbers of each type of venue on the x-axis.  The second is a horizontal bar chart restricted to coffee shops. These charts will be shown in the following section. 

Next, I performed a machine learning clustering algorithm on the full venue data obtained from Foursquare API.  I built a dataframe one hot encoding each of the over 200 venue categories, and similar to above, built a dataframe where each column counted the total occurrence of that venue type in a given neighborhood.  Using this data, I performed kmeans clustering to split the neighborhoods into 3 clusters based on prevalence of venue types.  These cluster labels were then applied to map labels to build a foilium map centered on Boston, which will be shown in the following section.  

# Results 

From the first bar chart we can see that Chinatown / Tufts - New England Medical Cener, Prudential, North End, West End / Back of the Hill and Brighton all have a high number of coffee shop adjacent venues.  This indicates that there is likely already market saturation in these neighborhoods, but it also indicates that these are neighborhoods that can support such a business. 

![](https://raw.githubusercontent.com/annahaensch/NeighborhoodViewer/master/barh1.png)

To further refine our analysis, we consider the bar chart below which only counts those venues in the category 'Coffee Shop.'  From this we see that Prudential, Chinatown / Tufts - New England Medical Cener, Beacon Hill all have 4 or more coffee shows (in addition, West End / Back of the Hill, Fenway / East Fens / Longwood, East Cambridge / Wellington - Harrington, and Brighton are in the next tier with 3 each), telling a slighly different story than the first graph.  In particular, North End is saturated with coffee shop adjacent business, but not necessarily with coffee shops themselves. 

![](https://raw.githubusercontent.com/annahaensch/NeighborhoodViewer/master/barh2.png)

From our clustering analysis, I used machine learning to cluster neighborhoods by venue type, as this is some sort of approximation of neighborhood character.  The results of the cluster analysis were added to the map of Boston below. 

![](https://raw.githubusercontent.com/annahaensch/NeighborhoodViewer/master/map.png)

The particular character of each of the neighrbood clusters was then analyzed by inspecting the dataframes grouped by cluster label.  In particular, the red cluster contains Chinatown / Tufts - New England Medical Cener, Prudential, Beacon Hill, West End / Back of the Hill and Back Bay, the latter of which which did not appear in the highest ranking neighborhoods for coffee shop adjacent businesses. 

# Discussion

Based on this analsys, Back Bay is a strong candidate for a coffee shop.  It currently only has 2 coffee shops, and only 9 coffee shop adjacent businesses.  In addition, it is most similar in character to the neighborhoods where coffee shops and coffee shop adjacent businesses are very popular.  This suggests some similalrity in locality and consumer tastes in the area.  Another neighborhood that might be strong candidates is Markets / Inner Harbor due to its clustering near the North End neighborhood; this neighborhood might warrant further analsysis. 

<p align="center">
  <img width="460" height="300" src="https://raw.githubusercontent.com/annahaensch/NeighborhoodViewer/master/BackBay.jpg">
</p>

<p align="center">
Shops in Boston's Back Bay neighborhood.  Image via <a href = https://commons.wikimedia.org/wiki/File:15-37_Newbury_Street_near_the_Public_Garden,_Boston,_Massachusetts.jpg>Wikimedia Commons</a>. 
<p>  


# Conclusion

The best neighborhood for opening a new coffee shop is one in which there is not currently a saturation of similar businesses, but where there is also neighborhood character that is similar enough to neighbrhoods where coffee shops have been successful.  This analsysis provides valuabled location and vanue information.  A further analysis should not be done to better understand the potential customers in each of the Boston/Cambridge neighborhoods, including housing costs and income. 
