Ansible Satellite 6 Install
===========================

Role to install and do basic configuration of Red Hat Satellite 6.X.  Really,
it handles Satellite Server 6.3 and probably up.

This role started off as Julio Villareal Pelegrino's role <julio@linux.com> but
there are quite a few changes made to accommodate Red Hat Satellite Server on EC2.

INFORMATION
-----------

This playbook will take a while to run depending the number of repositories to
sync.

Requirements
------------

You will need ansible and all the required subscriptions for RHEL 7 and
Satellite 6. Use ansible-galaxy to install the following playbooks:

- bennojoy.ntp
- zaxos.lvm-ansible-role

See the playbook-examples/requirements.yml file for an ansible-galaxy manifest.

You will need a subscription manifest that **matches the version of Red Hat
Satellite Server** you plan to install before getting started.

Role Variables
--------------

Base variables are in files located in ./vars and are imported with specifics
tasks.  These variables can be overwritten via an extra vars parameter like this:

    HOSTGROUP=satellite-server ansible-playbook -c local -i hosts -e '{satellite_deployment_vars: vars/local-vars.yml}' config.yml

In this example, config.yml is the "run list" for ansible-playbook to follow, and
vars/local-vars.yml is the list of variables that override settings in vars/main.yml.
See the playbook_example folder for the files you need to pass to ansible-galaxy
and ansible-playbook.

Tags
----

Tags can be run with `--include-tags` or skipped with `--skip-tags`.  Tags are:

| Tag | Purpose |
|-----|---------|
| backup | Set up a nightly backup script that copies data to Amazon S3. |
| capsule | Set up a Satellite Capsule server (completely untested as of now) |
| publish_content | Promote content-views of the content lifecycle |
| enable_repos | Enable redhat repos for satellite server to mirror |
| sync | Synchronize repos from Red Hat |
| email | Configure e-mail relaying and a daily report of host check-ins |
| install_satellite | For some reason you may want to skip installing satellite |
| install_software | For some reason you may want to skip installing additional software (utiliites) |
| rhn | register the system with RHN |

Dependencies
------------

There is no role dependency for this role.

Register with Red Hat
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

- Petr Balogh - <petr.balogh@gmail.com>
- Me :)
