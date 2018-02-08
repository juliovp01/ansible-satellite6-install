Ansible Satellite 6 Install
===========================

Role to install and do basic configuration of Red Hat Satellite 6.X.

INFORMATION
-----------

This playbook will take a while to run depending the number of repositories to
sync.

Requirements
------------

You will need ansible and all the required subscriptions for RHEL 7 and
Satellite 6. Also please use some role for set NTP on your server. We recommend
you use ansible-galaxy and install role for NTP **bennojoy.ntp** like we do.

Note that this example also uses **zaxos.lvm-ansible-role** just recently.

Role Variables
--------------

All variables are in files located in ./vars and are imported with specifics
tasks.

But to be open for others we decided specify only related variables there and
all mandatory variables you have to specify in playbook vars or pass in extra
vars parameter.

You can check default vars located in ./defaults/main.yml, where we specify
these variables you have to specify in your var file and overwrite them,
otherwise this role won't work properly.


Dependencies
------------

There is no role dependency for this role.

Inventory File
----------

The hosts file in playbook_examples simply uses the HOSTGROUP environment varialbe, like so:

```
HOSTGROUP=satellite-server ansible-playbook -i /tmp/ansible/hosts -e '{satellite_deployment_vars: /tmp/ansible/seed}' config.yml --skip-tags firewall,capsule,set_network -c local
```

How to run the playbook
------------------------

* To run the playbook first you need to create and download the manifest:

Go to <http://rhn.redhat.com>.
- Click "Satellite"
- Click "Register a Satellite"
- Set a Name, select a version and Click "Register"
After this we are going to  attach a subscription.
- Click "Attach Subscription" and select the subscription to attach and click
"Attach Selected"
After this we will download the manifest.
- Click "Download manifest"
After this copy the download file inside the /files directory on the role and
name it "satellite_manifest.zip"

** Then create the variable file in vars/your_name.yml in your playbook and
set all mandatory variables for role. You can inspire in vars/example-vars.yml.
And include this variable file in playbook as variable_files:

You can see example of playbook in playbook_example/config.yml

* Run the playbook, see README of example playbook

[playbook readme](./playbook_example/README.rst)

Problems
--------

TASK [satellite-deployment : RHN | subscribing to the right pool]
  - Remove the system from its attached subscription to redhat satellite, in the customer portal.

License
-------

MIT

Author Information
------------------

Julio Villarreal Pelegrino <julio@linux.com> more at: http://wwww.juliovillarreal.com

**Contributors:**

Petr Balogh - <petr.balogh@gmail.com>

