---
title: node start
---
<link rel="stylesheet" href="/global.css">

# bash 4 run node
```bash
#!/bin/sh

sudo setcap 'cap_net_bind_service=+ep' $(readlink -f $(which node))
npm start
```
