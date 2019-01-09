# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	# General Vagrant VM configuration.
	config.vm.box = "centos/7"
	config.ssh.insert_key = false
	config.vm.synced_folder ".", "/vagrant", disabled: true
	config.vm.provider :virtualbox do |v|
	  v.memory = 256
	  v.linked_clone = true
	end

	# Anisible controller server. 
	config.vm.define "node1" do |node1|
	  node1.vm.hostname = "node1"
	  node1.vm.network :private_network, ip: "192.168.60.4"
	end

	# Web server.
	config.vm.define "node2" do |node2|
	  node2.vm.hostname = "node2"
	  node2.vm.network :private_network, ip: "192.168.60.5"
	end
	 
	# Database server.
	config.vm.define "node3" do |node3|
	  node3.vm.hostname = "node3"
	  node3.vm.network :private_network, ip: "192.168.60.6"
	end

	config.vm.provision "ansible" do |ansible|
	  ansible.playbook = "playbook.yml" 
	end
end
