# project-visualizing-real-world-data-project

The aim of this project was to find the optimal location for the offices of our new company in the gaming industry, based on the information available in a unstructured database (*.json* available in folder "data") an tryin to match all the following criteria (the full project requirements can be found in *todos.md*):

- Designers like to go to design talks and share knowledge. There must be some nearby companies that also do design.
- 30% of the company have at least 1 child.
- Developers like to be near successful tech startups with that have raised at least 1 Million dollars.
- Executives like Starbucks A LOT. Ensure there's a starbucks not to far.
- Account managers need to travel a lot
- All people in the company have between 25 and 40 years, give them some place to go to party.
- Nobody in the company likes to have companies with more than 10 years in a radius of 2 KM.
- The CEO is Vegan
- Maintenance guy loves Basketball.

The project is divided in 2 folders. The **data** folder contains the datasets used in *.json* and *.csv* formats. The **my-code** folder contains the jupyter notebook files in which I did my data wrangling/cleaning and analysis. These should be read/executed in the following order:

**0. Clean, filter and geopoints:** here I made the query to the companies db in mongo db, creating new registers for each different office of each company. I cleaned the dataset and created binary variables identifying wether each company matches the specified criteria (age, type of company, succesful or not, etc.). I also created a "geo_point" field that could later be converted into a geo_index in mongo compass. The resulting dataframe was saved into a *.json*, available in the data folder.

**1. Analysis and location choice:** here I made a query to the new collection I created in the previus step, keeping only the "young" companies. Then, I made geoqueries for each of these companies to count the number of other "companies of interest" that where around them. Then, keeping only the companies with no "old" companies around, I scored the remaining companies based on the number of "desirable" companies they had around them. I then kept the top 50 companies and enriched the dataset with information obtained from the Google Places API, scoring each of the top 50 companies based on the number of "places of interest" they had around them (starbucks, schools, bars, vegan restaurants and international airports). I saved the resulting dataframe into a *.csv* (available in data folder) so I wouldn't have to call the API again if I closed the notebook.

I did my analysis based on the resulting dataframe and came to the conclusion that the best location for our offices would be in 34.081524, -118.382674 (located in West Hollywood, California, USA): https://goo.gl/maps/xewbhAdWuLSkG7zT7