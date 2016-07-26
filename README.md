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
In order to access the service you need to add an netry to /etc/hosts
```bash
$ echo "10.1.43.4 test.haproxy.local" | sudo tee -a /etc/hosts
```
Now everything should be set up. You can access your service at http://test.haproxy.local

Stats for HAProxy can be found at http://10.1.43.4:1963/haproxy?stats
Username and password for this UI is admin/password
