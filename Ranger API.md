This document is a collection of all the important Ranger API needed to troubleshoot Ranger issues.

Note: this document is under progress.

#### 1. ranger_audits Solr collection status
```bash
curl --negotiate -ik -u : "http://$(hostname -f):8886/solr/admin/collections?action=CLUSTERSTATUS&collection=ranger_audits&wt=json&indent=on"
```
