# Quick Prometheus tests

The goal here is to quickly validate the Jenkins Promethiums plugin and the
data and dashboards provided to Graphana.

# Starting up

1. run `docker-compose up`
2. go to http://localhost:3000
3. log in using username and password `admin/admin`
4. click skip (to not modify the password - this is a test system)
5. Click on `configure data source`
6. Slect `Prometheus`
7. In the URL, add `http://jenkins-monitoring_prom_1:9090`, this is the name of the docker container created.
8. click `save and test` - you should get a green `OK`
9. At the top, click on the dashboard icon.
10. Import all three dashboards.

Go from there.

This initial setup runs a node-exporter, graphana and promethius. It also collects
data from the node, prometheus itself and graphana.

#  To add Jenkins

In jenkins, we need to add the new plugin `prometheus-jenkins`

In the prometheus configuration, you must add the new scrapper.

```
- job_name: 'jenkins'
  metrics_path: '/prometheus/'
  scheme: http
  static_configs:
    - targets: ['jenkins-monitoring_jenkins_1:8080']
```

and finaly, in graphana, you must import a dashboard. The one tested has id `9524`
and also contains the initial configuration from above. See more at :
- https://grafana.com/dashboards/9524

Also :

- https://grafana.com/dashboards/9964

Both look good.
