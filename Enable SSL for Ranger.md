## Enable SSL on Ranger Admin UI using self-signed certificates

### 1. Stop all daemons in Ranger from Ambari

### 2. Create self-signed certificate in the Ranger admin host:
```cd /etc/ranger/admin/conf
keytool -genkey -keyalg RSA -alias ranger-admin -keystore ranger-admin-keystore.jks -storepass changeit -validity 360 0keysize 2048
```
In the above command, enter the FQDN of Ranger admin host for the 'Common Name' field (What is your first and last name).

### 3. Assign permissions and change ownership of the certificate to ranger
```chown ranger:ranger ranger-admin-keystore.jks
chmod 400 ranger-admin-keystore.jks
```

### 4. Define Ranger SSL properties in Ambari
- Uncheck **ranger.service.http.enabled** and ensure that the **External URL** points to _https_ and runs on port 6182 (default HTTPS port).
- **ranger.https.attrib.keystore.file**: the location of Ranger admin keystore file created above (/etc/ranger/admin/conf/ranger-admin-keystore.jks)
- **ranger.service.https.attrib.keystore.pass**: the keystore password entered above (changeit)
- **ranger.service.https.attrib.keystore.keyalias**: alias entered above (ranger-admin)
- **ranger.service.https.attrib.clientAuth**: want
- **ranger.service.https.attrib.ssl.enabled**: true
- **ranger.service.https.port**: 6182

### 5. Define custom Ranger SSL properties under 'Custom ranger-admin-site' in Ambari:
- **ranger.service.https.attrib.keystore.file**: should be the same as _ranger.https.attrib.keystore.file_
- **ranger.service.https.attrib.client.auth**: should be the same as _ranger.service.https.attrib.clientAuth_

### 6. Save changes and restart Ranger
