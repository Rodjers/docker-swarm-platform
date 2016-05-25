# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile for bootstrapping a development Consul cluster with
# VirtualBox provider and Ansible provisioner

VAGRANTFILE_API_VERSION = "2"
BOX_MEM = ENV['BOX_MEM'] || "1536"
BOX_NAME =  ENV['BOX_NAME'] || "debian/jessie64"
HOST_BASENAME = "test"
NUMBER_OF_HOSTS = 1

Vagrant.require_version ">= 1.5.0"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Configure 3 Consul nodes

  (1..NUMBER_OF_HOSTS).each do |i|
    config.vm.define "#{HOST_BASENAME}-#{i}" do |host_config|
      host_config.vm.box = BOX_NAME
      host_config.vm.network :private_network, ip: "10.1.42.#{i}"
      host_config.vm.hostname = "#{HOST_BASENAME}-#{i}"
      host_config.ssh.forward_agent = true
      host_config.vm.provider "virtualbox" do |v|
        v.name = "#{HOST_BASENAME}-#{i}"
        v.customize ["modifyvm", :id, "--memory", BOX_MEM]
        v.customize ["modifyvm", :id, "--ioapic", "on"]
        v.customize ["modifyvm", :id, "--cpus", "2"]
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      end
    end
    config.vm.provision "file", source: "files/ansible_rsa.pub", destination: "/home/vagrant/ansible_rsa.pub"
    config.vm.provision "shell", inline: "cat /home/vagrant/ansible_rsa.pub >> /home/vagrant/.ssh/authorized_keys"
  end
end
