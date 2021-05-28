import requests
import json
import pandas as pd

tag = requests.get(
    'https://api.stackexchange.com/2.2/tags?order=desc&sort=popular&site=stackoverflow')
tag_list = []

for data in tag.json()['items']:
    if data['has_synonyms'] == True:
        tag_list.append(data['name'])
        
elena = {}


for data in tag_list:
    link = 'https://api.stackexchange.com/2.2/tags/{}/synonyms?order=desc&sort=creation&site=stackoverflow'.format(data)
    same = requests.get(link)
    synonyms_list = []
    try:
        for syn in same.json()['items']:
            synonyms_list.append(syn['from_tag'])
            
        elena[data] = synonyms_list
    except:
        print(same.json())      
df = pd.DataFrame.from_dict(elena, orient = 'index')
df2 = df.iloc[:,[1,2,3,4]]
df2.columns = ["Synonym 1" , "Synonym 2" , "Synonym 3" , "Synonym 4"]
df2

