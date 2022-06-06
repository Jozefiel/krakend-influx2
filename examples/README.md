## Example
To load the extension into KrakenD you need to specify it in the extra_config section of the config:
```
"extra_config":{
...
    "telemetry/influx2": {
        "address": "http://influxdb:8086",
        "token": "eyJrIjoiN09MSVpVZjlVRG1xNHlLNApVbmZJOXFLWU1GOXFxNEIiLCJuIjoiD3Nzc3MiLCJpZCF6MX0",
        "org": "krakend-metrics",
        "bucket": "krakend",
        "batch_size": 50,
        "ttl": "30s"
    },
...
````
The necessary parameters are:

 - address - The url of the influxdb complete with port if different from http/https
 - token - Access token for organization/user
 - org - InfluxDB organization, workspace for a group of users
 - bucket - Named of location where time series data are stored
 - ttl - Expressed as \<value>\<units> , you can find accepted values here https://golang.org/pkg/time/#ParseDuration
 - batch_size - Set number of points sent in single request 

For this to work you need to have krakend-metric activated as well in extra_config:
```
...
    "github_com/devopsfaith/krakend-metrics": {
        "collection_time": "30s",
        "listen_address": "127.0.0.1:8090"
    }
...
```  
The collection_time and ttl parameters are strongly linked. The module krakend-metrics collects the metrics every **collection_time**, while krakend-influxdb checks every **ttl** if there are collected points to be sent.

You can find an example configuration in this folder as well as a dashboard JSON file for Grafana 5.0+.
 