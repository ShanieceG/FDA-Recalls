# FDA-Recalls
FDA Recalls going back 3 months that haven't been terminated yet

import pandas as pd
from bs4 import BeautifulSoup
import requests
url = "https://www.fda.gov/safety/recalls-market-withdrawals-safety-alerts"
recalls = pd.read_html(url)
df = recalls[0]
df
