# docker-swarm-platform
Ansible playbook to set up a five node Docker Swarm cluster (three managers and two workers) with two HAProxy loadbalancers with keepalived


## Dependencies
* Ansible 2.1
* Vagrant

## Getting started 
After cloning this repo you need to get the submodules which contains the roles.
```bash
$ git submodule init
$ git submodule update
```
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
In order to access the service you need to add an entry to /etc/hosts
```bash
$ echo "10.1.43.200 test.haproxy.local" | sudo tee -a /etc/hosts
```
Now everything should be set up. You can access your service at http://test.haproxy.local

Stats for HAProxy can be found at http://test.haproxy.local:1963/haproxy?stats
Username and password for this UI is admin/password
