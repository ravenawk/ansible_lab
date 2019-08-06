# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	# General Vagrant VM configuration.
	config.vm.box = "centos/7"
	config.ssh.insert_key = false
	config.vm.synced_folder ".", "/vagrant", disabled: true

	# Anisible controller server. 
	config.vm.define "node1" do |node1|
	  node1.vm.hostname = "node1"
	  node1.vm.network :private_network, ip: "192.168.60.4"
	  node1.vm.provider :virtualbox do |v1|
            v1.customize ['modifyvm', :id, '--memory', '4096']
            v1.customize ['modifyvm', :id, '--cpus', '2']
	  end
        end

	# Web server.
	config.vm.define "node2" do |node2|
	  node2.vm.hostname = "node2"
	  node2.vm.network :private_network, ip: "192.168.60.5"
	  node2.vm.provider :virtualbox do |v2|
            v2.customize ['modifyvm', :id, '--memory', '1024']
            v2.customize ['modifyvm', :id, '--cpus', '1']
	  end
        end
	 
	# Database server.
	config.vm.define "node3" do |node3|
	  node3.vm.hostname = "node3"
	  node3.vm.network :private_network, ip: "192.168.60.6"
	  node3.vm.provider :virtualbox do |v3|
            v3.customize ['modifyvm', :id, '--memory', '1024']
            v3.customize ['modifyvm', :id, '--cpus', '1']
  	  end
        end

	config.vm.provision "ansible" do |ansible|
	  ansible.playbook = "playbook.yml" 
	end
end
