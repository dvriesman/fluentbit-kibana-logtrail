
# My Fluentbit experience logging docker!


## Pre-requirements
- Elasticsearch

`
docker run --name elk -p 9200:9200 -p 9300:9300 -d docker.elastic.co/elasticsearch/elasticsearch-oss:6.6.0
`

## Optional - Build a customize Kibana docker image with Logtrail

Customize your kibana/logtrail.json and build your image:
`
docker build -t [your_account]/kibana:6.6.0 .
`

## Run your Kibana point to your elasticsearch

`
docker run --name kibana -p 5602:5601 -e ELASTICSEARCH_URL=http://myelastichost:9200 -d dvriesman/kibana:6.6.0
`

## Run fluentbit

`
docker run --name fluentbit --restart=always -p 24224:24224 -v `pwd`:/opt/bitnami/fluent-bit/conf -d bitnami/fluent-bit:latest
`

## Add new flag to docker gun

You should now add --log-driver=fluentd to all containers you want to log.

Example:

`
docker run --name mycontainer -d -p 8080:8080 --log-driver=fluentd dvriesman/myapp:1.0
`

Open you Kibana and you will see Logtrail in action !





