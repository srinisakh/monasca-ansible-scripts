#monasca-api
Installs the [monasca-api](https://github.com/stackforge/monasca-api) part of the [Monasca](https://wiki.openstack.org/wiki/Monasca) project.

##Requirements
- api_region 
- influxdb_url
- influxdb_user
- influxdb_password
- kafka_hosts - comma separated list of host:port combinations
- keystone_host
- keystone_admin
- keystone_admin_password
- mysql_host - SSL will be used if available
- mysql_user
- mysql_password
- zookeeper_hosts - comma separated list of host:port combinations

##Optional parameters
- keystone_admin_token - defaults to empty value
- keystone_admin_project - defaults to empty value
- monasca_api_client_port - the port the API listens on, default is 8080
- monasca_api_bind_host - if set, the port the API listens on is bound to this host or ip address
- monasca_admin_client_port - the port the admin connector listens on, default is 8081
- monasca_api_admin_bind_host - if set, the port the admin connector listens on is bound to this host or ip address

There is a truststore used by the application for any certificate authorities that must be trusted. Additionally there is a client
keystore for any ssl keys needed for client authentication. Most importantly there is a standard keystore used for serving the api
via ssl.

- monasca_api_keystore - The remote location to place the keystore. If this is defined SSL will be enabled for the API.
- monasca_api_keystore_src - The local location to copy the keystore from.
- monasca_api_keystore_password
- monasca_api_truststore - The remote location to place the truststore. Generally a truststore is needed for the keystone SSL CA.
- monasca_api_truststore_src - The local location to copy the truststore from.
- monasca_api_truststore_password
- monasca_api_client_keystore - The remote location to place the client keystore.
- monasca_api_client_keystore_src - The local location to copy the client keystore from.
- monasca_api_client_keystore_password

The keystore and truststore's are jks files and created by command such as these examples:

    # Change from pem to pkcs12 format 
    openssl pkcs12 -export -in orig.pem -inkey orig.key -out new.p12 -name fqdn -chain -CAfile cacert.pem -password pass:password
    # Create the jks keystore
    keytool -importkeystore -deststorepass password -destkeystore ./keystore.jks -srckeystore new.p12 -srcstoretype PKCS12 -srcstorepass password

##Example Playbook

    hosts: monasca
    sudo: yes
    roles:
      - {role: tkuhlman.monasca-api,
         influxdb_user: "{{api_influxdb_user}}",
         influxdb_password: "{{api_influxdb_password}}",
         mysql_user: "{{api_mysql_user}}",
         mysql_password: "{{api_mysql_password}}",
         tags: [api]}

##License
Apache

##Author Information
Tim Kuhlman
Monasca Team email monasca@lists.launchpad.net
