# CTProject

from bs4 import BeautifulSoup
import requests
import time
import pandas as pd

def rotten_movies():
    
    tomatoes_url = 'https://www.rottentomatoes.com'

    response = requests.get(tomatoes_url)

    html_doc = response.text

    soup = BeautifulSoup(html_doc, "lxml")

    data = soup.find('table', class_= 'movie_list', id='Top-Box-Office')

    time.sleep(2)
    
    return data.text

def punc(movies):
    for i in range (len(movies)):
        movies[i] = movies[i].replace('       ',',')
    return movies 
    
movies = rotten_movies()

file = open('rotten_movies_data', 'w')

file.write(f'{movies}\n ')

file.close()




df = pd.read_csv("rotten_movies_data")  
df.to_csv('D1.csv')

#audience score vs. tomato meter
#put into csv file, seperte by commas
#put into dataframe
#use pandas to visualize
