# -*- mode: ruby -*-
# vi: set ft=ruby :

boxname = 'centos/8'
servermb = '1024'
modecpuno = '1'

boxes = [
  {
    name: 'servera.example.com',
    ipv4net: '192.168.60.5',
  },
  {
    name: 'serverb.example.com',
    ipv4net: '192.168.60.6',
  },
  {
    name: 'serverc.example.com',
    ipv4net: '192.168.60.7',
  },
  {
    name: 'serverd.example.com',
    ipv4net: '192.168.60.8',
  },
]
    

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	# General Vagrant VM configuration.
	config.vm.box = boxname
	config.ssh.insert_key = false
	config.vm.synced_folder ".", "/vagrant", disabled: true

	# Main server with extra ram and cpu. 
        config.vm.define "workstation.example.com" do |workstation|
          workstation.vm.hostname = "workstation.example.com"
	  workstation.vm.network :private_network, ip: "192.168.60.4"
	  workstation.vm.provider :virtualbox do |v1|
            v1.customize ['modifyvm', :id, '--memory', '4096']
            v1.customize ['modifyvm', :id, '--cpus', '2']
	  end
        end

	# Create servers.
	boxes.each_with_index do |box, index|
	  config.vm.define box[:name] do |config|
	    config.vm.box = boxname
	    config.vm.hostname = box[:name]
	    config.vm.network :private_network, ip: box[:ipv4net]
	  config.vm.provider :virtualbox do |server|
            server.customize ['modifyvm', :id, '--memory', '2048']
            server.customize ['modifyvm', :id, '--cpus', '1']
	  end
        end
      end
	 
	config.vm.provision "ansible" do |ansible|
	  ansible.playbook = "playbook.yml" 
	end
end
