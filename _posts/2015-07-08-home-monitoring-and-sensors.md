---
title: Home monitoring and sensors
layout: post
type: post
status: publish
published: true
---

### I like dashboards
![everything]({{ site.url }}/assets/dashboard_full.png)
So I built one using [InfluxDB](https://influxdb.com/), [Grafana](http://grafana.org/), [Nginx](http://nginx.org/), [Tellstick Net](http://www.telldus.se/products/tellstick_net) and a bunch of scripts. Here's a breakdown of the parts and what feeds them.

### Temperatures
At home i have a Tellstick Net and a bunch of remotecontrolled power switches connected to this i also have a bunch of temperature sensors ([this model](http://www.lohelectronics.se/matinstrument/vaderstationer/tradlos-termometer-for-inneutomhusbruk.html)) places around the house, outside and in my shed.

### Logging to InfluxDB
Data is fed into InfluxDB using a couple of different scripts.  

* Temperatures are read from [Telldus Live](http://live.telldus.com/) using a [modified](https://gist.github.com/FredrikL/fe7cb4f214093f4c89cd) version of their [tdtool.py](http://developer.telldus.com/browser/examples/python/live/tdtool/tdtool.py) script every 10 minutes  
* To log status for my home server running ubuntu I [modified](https://github.com/FredrikL/status/blob/master/influx_status.rb) my status script, this is logged every 5 minutes.  
* Ping & packet loss is logged with a [simple](https://gist.github.com/FredrikL/a0f149414411c1874a53) ping script, right now it only pings googles public dns but is should be extended to ping multiple things (isp dns server etc) currently this script runs every minute  

### Improvements
I plan to add more fun sensors that work with Tellstick, things like rain and wind sensors. Something that logs how bright the sun is would be cool to. At some point when I have more info it will be fun to do some 'big data' stuff using the data set I have, right now it's been running for about 6 months so next year it's possible to graph current vs last year for many values.

