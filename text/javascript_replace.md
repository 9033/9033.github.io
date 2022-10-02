---
title: javascript replace
---
<link rel="stylesheet" href="/global.css">

# javascript replace  
1. replace  
    ```js
    s='aaaaa';
    t='a';
    c='b';
    s.replace(t,c);
    ```
    expected : "bbbbb"  
    but result : "baaaa"  
    only replaced first matched substring.😕  

2. RegExp  
    ```js
    s='aaaaa';
    t='a';
    c='b';
    r=new RegExp(t, "g");
    s.replace(r,c);
    ```
    expected : "bbbbb"  
    result : "bbbbb"  
    it's ok!!!!😄  

    but if input contains special character?   

    ```js
    s='a$aaaa';
    t='$a';
    c='b';
    r=new RegExp(t, "g");
    s.replace(r,c);
    ```
    expected : "abaaa"  
    but result : "a$aaaa"  
    it's bad...🤔

3. RegExp and encodeURIComponent  
    ```js
    s='a$aaaa';
    t='$a';
    c='b';
    s=encodeURIComponent(s);
    t=encodeURIComponent(t);
    c=encodeURIComponent(c);
    r=new RegExp(t, "g");
    decodeURIComponent(s.replace(r,c));
    ```
    expected : "abaaa"  
    result : "abaaa"  
    good!😁  

    but input special word of regular expression like dot?  

    ```js
    s='aaaaa...';
    t='.';
    c='b';
    s=encodeURIComponent(s);
    t=encodeURIComponent(t);
    c=encodeURIComponent(c);
    r=new RegExp(t, "g");
    decodeURIComponent(s.replace(r,c));
    ```
    expected : "aaaaabbb"  
    result : "bbbbbbbb"  
    😲  
    
4. split and join  
    found more simple way.  
    ```js
    s='aaaaa...';
    t='.';
    c='b';
    s.split(t).join(c);
    ```
    expected : "aaaaabbb"  
    result : "aaaaabbb"  
    it's simple and great.😎  
