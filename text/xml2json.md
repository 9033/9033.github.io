---
title: xml to json
---
<link rel="stylesheet" href="/global.css">

# xml to json
xml을 json으로 변환한다.  
```py
# python 3
from bs4 import BeautifulSoup
import json

def souptodict(soup):
    ret={}
    for child in soup.contents:
        if child.name==None:
            continue
        if child.string!=None:            
            ret[child.name]=child.string
        else:
            if child.name in ret:
                if type(ret[child.name])!=type([]):
                    ret[child.name]=[ret[child.name]]
                ret[child.name].append(t(child))
            else:
                ret[child.name]=t(child)
    return ret

def xmltojson(xml):
    soup=BeautifulSoup(xml,'html.parser')
    return json.dumps(souptodict(soup),indent=2)
```
