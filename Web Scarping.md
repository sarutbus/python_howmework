#package manager
!pip install gazpacho

#import function
import pandas as pd
import gazpacho
import requests

#Web scarping
url = "https://www.imdb.com/search/title/?groups=top_100&sort=user_rating,desc"
headers = {"Accept-Language": "en-US"}
html = requests.get(url,headers = headers)
imdb = gazpacho.Soup(html.text)

#prepare data for dataframe

#title
titles = imdb.find("h3", {"class": "lister-item-header"})
clean_title = [
    title.strip()[3:-7] for title in titles]

#ratings
ratings = imdb.find("div", {"class": "ratings-imdb-rating"})
ratings = imdb.find("div", {"class": "ratings-imdb-rating"})
clean_rating = [
    float(rating.strip()) for rating in ratings
    ]
