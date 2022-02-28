Vagrant.configure("2") do |config| 
    config.vm.box_check_update = "true"
    config.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
    end

    config.vm.define "r1" do |subconfig|
        subconfig.vm.box = "ubuntu/focal64"
        subconfig.vm.hostname = "r1"
        subconfig.vm.network :private_network,  ip: "172.16.0.100", netmask: "24", virtualbox__intnet: "peeringnetwork"
        subconfig.vm.network :private_network,  ip: "172.16.1.100", netmask: "24", virtualbox__intnet: "r1network"
        subconfig.vm.provider "virtualbox" do |vb|
            vb.customize ["modifyvm", :id, "--nictrace2", "on"]
            vb.customize ["modifyvm", :id, "--nictracefile2", "r1_peeringnetwork.pcap"]
        end
        subconfig.vm.provision "ansible" do |ansible|
            ansible.playbook="ansible/r1.yml"
        end
    end

    config.vm.define "r2" do |subconfig|
        subconfig.vm.box = "ubuntu/focal64"
        subconfig.vm.hostname = "r2"
        subconfig.vm.network :private_network,  ip: "172.16.0.200", netmask: "24", virtualbox__intnet: "peeringnetwork"
        subconfig.vm.network :private_network,  ip: "172.16.2.100", netmask: "24", virtualbox__intnet: "r2network"
        subconfig.vm.provider "virtualbox" do |vb|
            vb.customize ["modifyvm", :id, "--nictrace2", "on"]
            vb.customize ["modifyvm", :id, "--nictracefile2", "r2_peeringnetwork.pcap"]
        end
        subconfig.vm.provision "ansible" do |ansible|
            ansible.playbook="ansible/r1.yml"
        end
    end

    config.vm.define "pmacct" do |subconfig|
        subconfig.vm.box = "ubuntu/focal64"
        subconfig.vm.hostname = "pmacct"
        subconfig.vm.network :private_network,  ip: "172.16.0.250", netmask: "24", virtualbox__intnet: "peeringnetwork"
        subconfig.vm.provider "virtualbox" do |vb|
            vb.customize ["modifyvm", :id, "--nictrace2", "on"]
            vb.customize ["modifyvm", :id, "--nictracefile2", "pmacct_peeringnetwork.pcap"]
        end
        subconfig.vm.provision "ansible" do |ansible|
            ansible.playbook="ansible/pmacct.yml"
        end
    end
end
