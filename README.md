Ansible Satellite 6 Install
===========================

Role to install and do basic configuration of Red Hat Satellite 6.X. 

INFORMATION
-----------

This playbook will take a while to run depending the number of repositories to sync.

Requirements
------------

You will need ansible and all the required subscriptions for RHEL 7 and Satellite 6. 

Role Variables
--------------

All the variables are on /var/main.yml



Dependencies
------------

There is no role dependency for this role.

Host File
----------

The host file for this role is hosts.target and the format is: 

[satellite]
IP FOR SATELLITE SERVER

How to run the playbook
------------------------

** To run the playbook first you need to create and download the manifest: 

Go to rhn.redhat.com. 
- Click "Satellite"" 
- Click "Register a Satellite"
- Set a Name, select a version and Click "Register"
After this we are going to  attach a subscription. 
- Click "Attach Subscription" and select the subscription to attach and click "Attach Selected"
After this we will download the manifest. 
- Click "Download manifest"
After this copy the download file inside the /files directory on the role and name it satellite_manifest.zip 

** Then edit the variable file on vars/main.yml to set it to your environment. 

** Run the playbook

ansible-playbook -i hosts.target satellite.yaml


License
-------

MIT

Author Information
------------------

Julio Villarreal Pelegrino <julio@linux.com> more at: http://wwww.juliovillarreal.com
