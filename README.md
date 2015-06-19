# Elasticsearch, Logstash, Kibana (ELK)

Configured to use redis as a message broker for logstash, based on
[sebp/elk](https://registry.hub.docker.com/u/sebp/elk/).

## Ports
When run as a container the image exposes the following ports:

* 5601 - Kibana web interface
* 9200 - Elastic search interface

## Important Files

* `Dockerfile` - Dockerfile to build the ELK image
* `logstash.conf` - Logstash configuration
* `elasticsearch.yml` - Elastic search configuration
* `start.sh` - Runs all services and tails the elasticsearch logs.

## Environment Variables

Environment variables are not supported by default for logstash configurations
however we have added limited support for them by modifying the `start.sh`.
If you want to introduce a new variable to a configuration perform the following
steps:

1. Add the placeholder for the variable in the file. It will look like this:
`{{MY_VARIABLE}}`
2. Modify the `start.sh` script to add an in-place sed to replace the placeholder
with the environment variable:
`sed -i "s/{{MY_VARIABLE}}/$MY_VARIABLE/g" /etc/logstash/conf.d/01-logstash.conf`.

Currently we support the following environment variables in the logstash
configuration script:

* `REDIS_HOST` - Hostname for the redis message broker.
