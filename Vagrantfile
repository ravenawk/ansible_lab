# -*- mode: ruby -*-
# vi: set ft=ruby :

boxname = 'centos/7'
nodemb = '1024'
modecpuno = '1'

boxes = [
  {
    name: 'node2',
    ipv4net: '192.168.60.5',
  },
  {
    name: 'node3',
    ipv4net: '192.168.60.6',
  },
]
    

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	# General Vagrant VM configuration.
	config.vm.box = boxname
	config.ssh.insert_key = false
	config.vm.synced_folder ".", "/vagrant", disabled: true

	# Main node with extra ram and cpu. 
	config.vm.define "node1" do |node1|
	  node1.vm.hostname = "node1"
	  node1.vm.network :private_network, ip: "192.168.60.4"
	  node1.vm.provider :virtualbox do |v1|
            v1.customize ['modifyvm', :id, '--memory', '1024']
            v1.customize ['modifyvm', :id, '--cpus', '1']
	  end
        end

	# Create nodes.
	boxes.each_with_index do |box, index|
	  config.vm.define box[:name] do |config|
	    config.vm.box = boxname
	    config.vm.hostname = box[:name]
	    config.vm.network :private_network, ip: box[:ipv4net]
	  config.vm.provider :virtualbox do |node|
            node.customize ['modifyvm', :id, '--memory', '1024']
            node.customize ['modifyvm', :id, '--cpus', '1']
	  end
        end
      end
	 
	config.vm.provision "ansible" do |ansible|
	  ansible.playbook = "playbook.yml" 
	end
end
