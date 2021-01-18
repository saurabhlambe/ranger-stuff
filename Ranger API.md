This document is a collection of all the important Ranger API needed to troubleshoot Ranger issues.

Note: this document is under progress.

#### 1. ranger_audits Solr collection status
```bash
curl --negotiate -ik -u : "http://$(hostname -f):8886/solr/admin/collections?action=CLUSTERSTATUS&collection=ranger_audits&wt=json&indent=on"
```

#### 2. Fetch Ranger service repository
```bash
curl -u admin:admin http://localhost:6080/service/public/api/repository/3 -H 'Content-Type:application/json' > old-hive-service.json
```
