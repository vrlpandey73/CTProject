from bs4 import BeautifulSoup 

import requests

import time

import pandas as pd

import matplotlib.pyplot as plt




def top_box_office():
    
    url = "https://www.rottentomatoes.com/browse/box-office/"

    response = requests.get(url)

    html_doc = response.text

    soup = BeautifulSoup(html_doc, "lxml")

    table = soup.find('table', class_='center table')

    table_rows = table.find_all('tr', itemprop='itemListElement')

    row =[]

    for tr in table_rows:

        td = tr.find_all('td')

        row.append([i.text for i in td])

    time.sleep(3)

    return row


def create_dataframe(list):

    for i in list:

        dataframe= pd.DataFrame(list[0:], columns=list[0])

        dataframe.columns = ['This_Week', 'Last_Week', 'Tmeter', 'Title', 'Weeks_Released','Weekend_Gross','Total_Gross', 'Theater_Avg.', '#_of_theater']
        
    return dataframe



x = top_box_office()

print(x)

y = create_dataframe(x)
y['Weekend_Gross (in millions)'] = y.Weekend_Gross.str.replace(r"[M,$]",'')
y['Tmeter'] = y['Tmeter'].str.extract('(\d+)', expand=False)


y.to_csv('file.csv')

    
dfx = pd.read_csv('file.csv')

df_fil = dfx[['Tmeter']]

print(df_fil.describe())
'''
plt.figure()
y['Weekend_Gross'].hist()
plt.xlabel('Revenue')
plt.ylabel('Title')
plt.savefig('WeekendRev.jpg')
'''

#def millions(y['Total_Gross']):
    #for i in y['Total_Gross']:
       # if 
a = dfx['Tmeter']
plt.ylabel('Ratings in %')
plt.title('Summary Statistics of Tomato Meter')
a.plot.box()

y['Tmeter'] = y.Tmeter.astype('int64')

y.loc[y['Tmeter'] > 60,['Tmeter','Title']]




