# vagrant-wordpress
Systems Engineer Test Task

Deploys a WordPress-based website running on 2 virtual machines (Ubuntu 16.04) with the help of Vagrant and Ansible tools. 
The access to the website is protected by [Online LDAP Test Server](https://www.forumsys.com/tutorials/integration-how-to/ldap/online-ldap-test-server/).

## Requirements

- [Ansible](http://www.ansible.com)
- [Vagrant](http://www.vagrantup.com)
- [VirtualBox](http://www.virtualbox.org)

## Usage

Run `vagrant up` to create and provision virtual machines.
Then, open http://172.29.1.10 via browser on the host machine and provide valid credentials.

All required software for running the website is being installed on VMs
dependently on theirs roles (There are 4, currently)

The user ‘serviceuser’ will be created on both VMs with ‘sudo’ permissions allowing to manage
services.

## Config

Some settings can be adjusted in vars/default.yml file (Not fully implemented yet, some hardcode stil persists)
Main Playbook.yml is used to assign roles to VM groups.
