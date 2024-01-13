# highcharts-export-docker

This repo now contains a dockerfile used to build a docker image of the highcharts export server version 3.

The dockerfile is based on (a reverse engineered) docker image by cubetiq/highcharts-export-server of the official docker hub.

Fortunately we no longer require a fork of the npm package to include pie chart support, this is included in the standard image.

If you want to skip the build phase and get a container running there is an automatic build setup on dockerhub. Any commits to this repo will automatically build a new container here:

https://hub.docker.com/r/andyhirdcml/highcharts-export-node-pie/

this is a pie chart version of:

https://hub.docker.com/r/onsdigital/highcharts-export-node/

## Build Locally

```
docker build -t highcharts-export-server .
```

Note that this has problems on macos. It looks like chromium or puppeteer don't work unless (most likely) it's done on Intel hardware.

## Run Locally

```
docker run -d --name highcharts -p 8889:8080 highcharts-export-server
```
The above command will expose the service on port 8889. This can be changed if required.

## Test

Once the server is running here is an example curl command to render a chart:
```
curl -H "Content-Type: application/json" -X POST -d '{"infile":{"title": {"text": "Steep Chart"}, "xAxis": {"categories": ["Jan", "Feb", "Mar"]}, "series": [{"data": [29.9, 71.5, 106.4]}]}}' 127.0.0.1:8889 -o testchart.png
```
