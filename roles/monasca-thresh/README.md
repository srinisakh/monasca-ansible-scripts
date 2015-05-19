#monasca-thresh
Installs the [monasca-thresh](https://github.com/stackforge/monasca-notification) part of the [Monasca](https://wiki.openstack.org/wiki/Monasca) project.
Monasca-thresh requires storm to be running and should be installed on the nimbus box.

##Requirements
- kafka_hosts - comma separated list of host:port pairs.
- mysql_host - By default ssl will be used if available.
- mysql_user
- mysql_password
- zookeeper_hosts - comma separated list of host:port pairs.

##License
Apache

##Author Information
Tim Kuhlman
Monasca Team email monasca@lists.launchpad.net
