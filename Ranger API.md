This document is a collection of all the important Ranger API needed to troubleshoot Ranger issues.

Note: this document is under progress.

#### 1. ranger_audits Solr collection status
```bash
curl --negotiate -ik -u : "http://`hostname -f`:8886/solr/admin/collections?action=CLUSTERSTATUS&collection=ranger_audits&wt=json&indent=on"
```

#### 2. Fetch Ranger service repository
```bash
curl -u admin:admin http://`hostname -f`:6080/service/public/api/repository/{ID} -H 'Content-Type:application/json' > old-hive-service.json
```

#### 3. Download policies in a repository
```bash
curl -iv -k --negotiate -u : -H "Content-type:application/json" -X GET "https://`hostname -f`:6182/service/plugins/secure/policies/download/<reponame>"
```

#### 4. Fetch a user's role
```bash
curl -s -u admin:hadoop12345! -H "Accept: application/json" -H "Content-Type: application/json" -X GET http://`hostname -f`:6080/service/xusers/users/24 > /tmp/curl.out
```

#### 5. Change the role of a user to _Admin_ or vice versa
```bash
curl -u admin:hadoop12345! -v -i -s -X PUT -H "Accept: application/json" -H "Content-Type: application/json" http://`hostname -f`:6080/service/xusers/secure/users/24 -d @/tmp/curl.out
```
> There are two roles in Ranger: ROLE_USER and ROLE_SYSADMIN. Replace the roles in the curl.out file above accordingly.
