#Satellite deployment

This playbook install all dependecies required by satellite, register RHN,
install satellite, and create some basic configuration of satellite.

##Configuration

You have to specify a lot of variables for satellite-deployment role.
This playbook assumes that you set all these variables in some variable file
and its path you have to pass as parameter: ``satellite-deployment-vars``

##Parameters

- **satellite-deployment-vars**
    This parameter should contains path to variable file which will describe
    all related variables for your Satellite server.
    For example: ./vars/brq-sat-instance.yml which is relative path from
    playbook.
    You can see examples in [example-vars.yml](./vars/example-vars.yml)


##Requirements

- requirements are defined in [requirements.yml](./requirements.yml)
- for instll all requirements pleas run:
``ansible-galaxy install -f -r requirements.yml -p roles/``

##Execution

- For execute playbook with whole process of deployment run:
  ``ansible-playbook -u root -i host.target -e
  '{satellite_deployment_vars: ./vars/path_to_your_vars.yml}' ./config.yml``

- You can also only update or run specific ation with scpecify appropriate
  tags:
``ansible-playbook -u root -i host.target -e
  '{satellite_deployment_vars: ./vars/path_to_your_vars.yml}'
  --tags=update_stallite ./config.yml``

you can also exclude some tags with ``--skip-tags`` parameter of
ansible-playbook command.

##Tags

- **capsule**: configure a capsule
- **email**: configure e-mail settings (SMTP relay server, email for admin user)
- **enable_repos**: deploy repositories
- **firewall**: set firewall
- **install**: install additional software  
- **install_satellite**: install satellite
- **publish_content**: publish/promote a version of the default content view, which takes a long time
- **rhn**: register rhn
- **set_network**: actually configure network settings
- **ssl**: import a custom SSL certificate
- **sync**: sync repo content, which takes just shy of an eternity
- **update_satellite**: update satellite
