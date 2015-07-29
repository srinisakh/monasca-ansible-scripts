etup devstack
 
Setup devstack on the machine as you normally do using information from http://docs.openstack.org/developer/devstack/

### Download ansible script repo

	git clone git@gitlab.gozer.hpcloud.net:mnb-ceilometer/monasca-ansible-scripts.git

**Install ansible**
	
	sudo apt-get install ansible
	
ansible version > 1.8 recommended

If it is not follow the steps outlined here to upgrade ansible http://docs.ansible.com/ansible/intro_installation.html#latest-releases-via-apt-ubuntu

	$ ansible --version
	ansible 1.9.1
	configured module search path = None

### Edit /etc/hosts add following line

	127.0.0.1       devstack mini-mon localhost

### Required in case of using password access to SSH 
	
	sudo apt-get install sshpass

### Run the minified devstack - removed monasca-ui and monasca-devstack roles from it

	ansible-playbook -u metering --sudo --ask-sudo-pass -k -i inventory_devstack devstack.yml


### Run mini-mon to setup monasca

	ansible-playbook -u metering --sudo --ask-sudo-pass -k -i inventory_minimon mini-mon.yml
	
### Troubleshooting
	
**If you receive following host key check failure**
	
	fatal: [devstack] => Using a SSH password instead of a key is not possible because Host Key checking is enabled and sshpass does not support this.  Please add this host's fingerprint to your known_hosts file to manage this host.
 
try running the below commands as SUDO

	ssh localhost
	ssh devstack
	ssh mini-mon
 
	This will add the key to the known hosts
	
**If you get Keystone unauth error**

	TASK: [monasca-keystone | Keystone Service - Execute the script] **************
 
	Edit keystone_admin_token in group_vars/all to supply the correct token value

### Kafka troubleshooting
When restarting kafka also restart zookeeper
