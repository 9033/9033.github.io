---
title: node start
---
<style >body {background-color:lightblue;}</style>
# bash 4 run node
```bash
#!/bin/sh

sudo setcap 'cap_net_bind_service=+ep' $(readlink -f $(which node))
npm start
```
