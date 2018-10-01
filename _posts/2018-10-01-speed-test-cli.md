---
layout: post
title: Visualizing speedtest-cli Data
---

![Speed Test Data](https://i.imgur.com/3MDFtva.png)

Github Repository for speedtest-cli: [link](https://github.com/sivel/speedtest-cli)

```python
import os
import re
import subprocess
import time

response = subprocess.Popen('speedtest-cli --simple', shell=True, stdout=subprocess.PIPE).stdout.read()

ping = re.findall('Ping:\s(.*?)\s', response, re.MULTILINE)
download = re.findall('Download:\s(.*?)\s', response, re.MULTILINE)
upload = re.findall('Upload:\s(.*?)\s', response, re.MULTILINE)

ping[0] = ping[0].replace(',', '.')
download[0] = download[0].replace(',', '.')
upload[0] = upload[0].replace(',', '.')

try:
    if os.stat('/samba/data/speedtest.csv').st_size == 0:
        print 'Date,Time,Ping (ms),Download (Mbit/s),Upload (Mbit/s)'
except:
    pass

@

```

This code writes to a CSV in a SMB share called speedtest.csv

When I created the scatterplot above I converted to an xlsx and selected the data and inserted the chart.
