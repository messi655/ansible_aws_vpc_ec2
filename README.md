This Ansible Playbook will help you create a AWS VPC and Create EC2 Instances

# Purpose

This role setups the following:

* VPC
* Two networks(private and public)
* Create instance in public and instances in private and assign public IP for public instance
* Adds internet gateway and NAT gateway to allow communication between networks and internet
* General hosts group by change environment path to hosts group: path_hosts_group
* Allows to cleanup VPC and all created AWS resources

# Require
- Create ssh key pair and put public key in roles/create_ec2_vpc/files

# Usage
## Change the parameter match with your requirement!
* Edit file all.yml in group_vars

## Choose mode for your system

Edit file playbook.yml

* Multi AZ: 
```
roles:
    - { role: create_ec2_vpc, mutiAZ: "yes", tags: [ "create" ] }
    - { role: clean-ec2-vpc, mutiAZ: "yes", tags: [ "clean" ] }
```
* Single AZ:
```
roles:
    - { role: create_ec2_vpc, mutiAZ: "no", tags: [ "create" ] }
    - { role: clean-ec2-vpc, mutiAZ: "no", tags: [ "clean" ] }
```

## Authentication with AWS
* http://docs.ansible.com/ansible/latest/guide_aws.html

## Create
* $ansible-playbook playbook.yml --tags=create

## Clean
* $ansible-playbook playbook.yml --tags=clean


