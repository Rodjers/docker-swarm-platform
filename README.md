# docker-swarm-platform
Ansible playbook to set up a two node Docker Swarm cluster with one HAProxy loadbalancer


## Dependencies
* Ansible 2.1
* Vagrant

## Getting started 
Run this command to set up the hosts with Vagrant
```bash
$ vagrant up
```
Set correct permissions on the private key for Ansible
```bash
$ chmod 600 files/ansible_rsa
```
Run this command to provision your machines with Ansible
```bash
$ ansible-playbook site.yml
```
