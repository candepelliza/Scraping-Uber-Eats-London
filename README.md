# Scraping London Uber Eats Data

A python code for scraping data about Uber Eats restaurants in London. The code was based on the  [Extreme Uber Eats Scraping Project](https://github.com/gsunit/Extreme-Uber-Eats-Scraping) from @gsunit, but adapted and simplified for its application in London Uber Eats website. 
The scraped data is also available for download.

## Folder structure

 - `/notebooks` contains the scraping scripts as Jupyter Notebooks
      - `/notebooks/1-London-categories` script for obtaining all restaurant categories, with the urls and number of restaurants in each one
      - `/notebooks/2-London-restaurant-urls` script for obtaining all restaurants' urls
      - `/notebooks/3-London-restaurant-details` script for obtaining the details of all existing restaurants
 - `/scraped-data` contains all the scraped data city-wise
    - `/scraped-data/1-London-cat-all` csv file containing the name of all existing categories, with the respective url and number of restaurants
    - `/scraped-data/2-London-rest-all` csv file containing the urls of all existing restaurants for all the categories
    - `/scraped-data/3-London-rest-details-all` csv file containing the details for each existing restaurant


## Code structure

The code is organized in three different notebooks, corresponding to three scraping steps. Each notebook generates a csv file that is then used as an input for the next step.

### 1 - Extracting Categories' urls

The first step cosists on obtaining all the existing categories in London Uber Eats website, and the corresponding link for each one. The code takes as input the url of Uber Eats London homepage. 

The result of this script is the '1-London-cat-all' csv file, which has 3 columns: 

   `url` url of the category mainpage
   
   `rest_num` number of restaurants inside that category. It is important to noticce that restaurants usually are tagged with more than 1 category, meaning that the summatory of all `rest_num` values is much bigger than the actual number of existing restaurants

   `category` category name

Notebook file: `/1-London-categories.ipynb`

Input: Uber Eats London homepage url https://www.ubereats.com/gb/category/london-eng

Output: `/1-London-cat-all.csv`


### 2 - Getting a list of all city restaurants

Based on the list of categories' urls, the second step scraps the restaurants inside each category and creates a unique list with the urls. Having an unique list allows preventing the repetition of restaurants tagged with more than one category and simplifies the process for the detail scraping in the third step. 

The result of this script is the '2-London-rest-all' csv file which has only 1 column:

   'urls' url of a restaurant in the website

Notebook file: `/2-London-restaurant-urls.ipynb`

Input: `/1-London-cat-all.csv`

Output: `/2-London-rest-all.csv`


### 3 - Getting restaurant details

The final step is the one that truly scraps restaurants details and, for that very reason, is the most time consuming. The script uses the url list to acess each restaurant page and, through the json object of each one, get the restaurant details. For this script, some of the available details, such as menu and opening hours were not obtained, focusing on the main interest aspects, but they could be also scrapped.

The result of this script is the '3-London-rest-details-all' csv file which has 12 columns:

   'name': restaurant complete name

   'url': link to the restaurant page in uber eats website

   'cuisine': category tags of the restaurant (can be more than one)

   'avgRating': restaurant rating calculated as the mean value of all restaurant clients' ratings

   'priceRange': estimated indicator of price range, as '€' (cheap), '€€' (medium) or '€€€' (expensive)

   'latitude': latitude coordinates

   'longitude': longitude coordinates

   'postalCode': location postal code

   'streetAddress': adress street name and number

   'addressLocality': adress locality or neighborhood name

   'addressRegion': adress region name

   'addressString': complete adress compose by addressLocality, addressRegion, postalCode, addressCountry and streetAddress

Notebook file: `/3-London-restaurant-details`

Input: `/2-London-rest-all.csv`

Output: `/3-London-rest-details-all.csv`
