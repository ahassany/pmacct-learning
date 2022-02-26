Vagrant.configure("2") do |config| 
    config.vm.box_check_update = "true"
    config.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
    end

    config.vm.define "r1" do |subconfig|
        subconfig.vm.box = "ubuntu/focal64"
        subconfig.vm.hostname = "r1"
        #subconfig.vm.network :private_network,  type: "dhcp"
        subconfig.vm.network :private_network,  ip: "172.16.0.100", netmask: "24", virtualbox__intnet: "peeringnetwork"
        subconfig.vm.network :private_network,  ip: "172.16.1.100", netmask: "24", virtualbox__intnet: "r1network"
        subconfig.vm.provision "ansible" do |ansible|
            ansible.playbook="ansible/r1.yml"
        end
    end

    config.vm.define "r2" do |subconfig|
        subconfig.vm.box = "ubuntu/focal64"
        subconfig.vm.hostname = "r2"
        #subconfig.vm.network :private_network,  type: "dhcp"
        subconfig.vm.network :private_network,  ip: "172.16.0.200", netmask: "24", virtualbox__intnet: "peeringnetwork"
        subconfig.vm.network :private_network,  ip: "172.16.2.100", netmask: "24", virtualbox__intnet: "r2network"
        subconfig.vm.provision "ansible" do |ansible|
            ansible.playbook="ansible/r1.yml"
        end
    end
end
