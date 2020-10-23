2018-10-01 <a style='cursor:pointer;' onclick='document.querySelector("#t20181001").style.display=""'>aaa</a>  

<t id='t20181001' style='display:none;'>
<pre>
//javascript
getimgs=(doc)=>{
    images=[...doc.images];
    subdocs=[...doc.querySelectorAll('frame')].map(f=>f.contentDocument);
    subdocs.forEach(c=>images=images.concat([...c.images]));
    return images;
};
document.querySelector('html').innerHTML=getimgs(document).map(s=>s.outerHTML).join('');
</pre>
</t>  

```js
//javascript
getimgs=(doc)=>{
    images=[...doc.images];
    subdocs=[...doc.querySelectorAll('frame')].map(f=>f.contentDocument);
    subdocs.forEach(c=>images=images.concat([...c.images]));
    return images;
};
document.querySelector('html').innerHTML=getimgs(document).map(s=>s.outerHTML).join('');
```
<script src="https://gist.github.com/9033/40524bc5a2680acdae0742e65ad067be.js"></script>
