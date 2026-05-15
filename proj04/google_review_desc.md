---
layout: page
title: Hawaii Google Maps Reviews 🏝️
description: Description of the Hawaii Google Maps reviews dataset in Project 4.
parent: 📊 Final Project
nav_exclude: true
---

# Hawaii Google Maps Reviews 🏝️
This dataset contains Google Maps reviews of various locations in Hawaii. It was originally scraped and used by the authors of these papers: https://aclanthology.org/2022.acl-long.426.pdf, https://arxiv.org/pdf/2207.00422. The full dataset is quite long, so we will only be using the 10-core one.


## Getting the Data
There are two files: 

`review-Hawaii_10.json.gz`
[Link](https://mcauleylab.ucsd.edu/public_datasets/gdrive/googlelocal/review-Hawaii_10.json.gz)

| Column | Description |
|:---|:---|
| `user_id` | ID of the reviewer |
| `name` | name of the reviewer |
| `time` | time of the review (unix time) |
| `rating` | rating of the business |
| `text` | text of the review |
| `pics` | pictures of the review |
| `resp` | business response to the review including unix time and text of the response |
| `gmap_id` | ID of the business |

`meta-Hawaii.json.gz` 
[Link](https://mcauleylab.ucsd.edu/public_datasets/gdrive/googlelocal/meta-Hawaii.json.gz)

| Column | Description |
|:---|:---|
| `name` | name of the business |
| `address` | address of the business |
| `gmap_id` | ID of the business |
| `description` | description of the business |
| `latitude` | latitude of the business |
| `longitude` | longitude of the business |
| `category` | category of the business |
| `avg_rating` | average rating of the business |
| `num_of_reviews` | number of reviews |
| `price` | price of the business |
| `hours` | open hours |
| `MISC` | MISC information |
| `state` | the current status of the business (e.g., permanently closed) |
| `relative_results` | relative businesses recommended by Google |
| `url` | URL of the business |

You can read more about the datasets [here](https://mcauleylab.ucsd.edu:8443/public_datasets/gdrive/googlelocal/).  
Note that these datasets are zipped (`.gzip`) and are `.json`s instead of `.csv` files. It is recommended to unzip them manually first, and then use `pd.read_json` to turn it into a pandas DataFrame. You will also have to add the argument `lines=True` since the data is one json object per line. It is also recommended to use `engine='pyarrow'` to speed up reading.  
`pd.read_json(path, lines=True, engine='pyarrow')`

## Example Questions and Prediction Problems
Feel free to base your exploration into the dataset in Steps 1-4 around one of these questions, or come up with a question of your own.

- What location category has the lowest reviews? Highest number of reviews? What insight can you extract from this information?
- Position yourself as someone who wants to open a business in Hawaii. Using the data provided, can you generate some insight into what makes a successful business? To try to answer this question, you could focus on one category or zip code.
- What are the most common words in restaurant names? Do certain names correlate with higher ratings?
- Look up particularly trendy/touristy areas in Hawaii. Do zip codes in these areas tend to have higher ratings? Higher prices? More number of reviews?
- How do business response behaviors (response rate, response time, and response sentiment) influence future customer ratings and review volume? This could help determine whether active customer engagement measurably improves business performance.

Feel free to use one of the prompts below to build your predictive model in Steps 5-8, or come up with a prediction task of your own.

- Predict a location's rating based on its zip code, ratings, and/or other features. This could help prospective business owners gauge their chance of success.
- Predict whether a business is at risk of becoming permanently closed.
- Predict whether a business will respond to a customer review and estimate the response delay. This models customer engagement practices at the business level.
- If you are interested in recommender systems: predict which businesses a user is most likely to review highly.

## Special Considerations
- The dataset we provide here was reduced to extract the 10-core, such that each of the remaining users and items have 10 reviews each. You should think about how this effects any analyses you do and what kind of biases might be introduced. 
- Make sure to inspect the data type/format of each column. You might find some of them are oddly formatted compared to what you have encountered in DSC80 so far. Clean them and you might be able to extract more useful features.
- If you plan to use geographical features, you should think about how to feed those features into your model. Can you use raw latitude/longitude directly? Or maybe it's better to one-hot encode the zip codes instead? Maybe you could engineer features like distance to downtown or the beach? Or run some sort of clustering algorithm like K-means?