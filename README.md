# CTProject

from bs4 import BeautifulSoup
import requests
import time

def rotten_movies():
    
    tomatoes_url = 'https://www.rottentomatoes.com'

    response = requests.get(tomatoes_url)

    html_doc = response.text

    soup = BeautifulSoup(html_doc, "lxml")

    data = soup.find('table', class_= 'movie_list', id='Top-Box-Office')

    time.sleep(2)
    
    return data.text
    
movies = rotten_movies()

file = open('rotten_movies_data', 'w')

file.write(f'{movies}\n ')

file.close()

#audience score vs. tomato meter
#put into csv file, seperte by commas
#put into dataframe
#use pandas to visualize
