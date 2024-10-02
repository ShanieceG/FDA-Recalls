# FDA-Recalls
FDA Recalls going back 3 months that haven't been terminated yet

import pandas as pd
from bs4 import BeautifulSoup
import requests

url = "https://www.fda.gov/safety/recalls-market-withdrawals-safety-alerts"
page = requests.get(url)
soup = BeautifulSoup(page.content, "html.parser")

rows = soup.find('table', {'id':'datatable'}).find('tbody').find_all('tr')

recall_list = []
for row in rows:
    dic = {}
    dic['Date'] = row.find_all('td')[1].text
    dic['Brand Name(s)'] = row.find_all('td')[2].text
    dic['Product Description'] = row.find_all('td')[3].text
    dic['Recall Reason Description'] = row.find_all('td')[4].text
    dic['Company Name'] = row.find_all('td')[5].text
    dic['Teminated Recall'] = row.find_all('td')[6].text
    recall_list.append(dic)
    
df = pd.DataFrame(recall_list)
df
