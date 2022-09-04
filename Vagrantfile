Vagrant.configure("2") do |config| 
    config.vm.box_check_update = "true"
    config.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
    end

    config.vm.define "r1" do |subconfig|
        subconfig.vm.box = "ubuntu/focal64"
        subconfig.ssh.forward_agent = true
        subconfig.ssh.forward_x11 = true
        subconfig.vm.hostname = "r1"
        subconfig.vm.network :private_network,  ip: "172.16.0.10", netmask: "24", virtualbox__intnet: "peeringnetwork"
        subconfig.vm.network :private_network,  ip: "172.16.1.10", netmask: "24", virtualbox__intnet: "r1network"
        subconfig.vm.network :private_network, ip: "192.168.56.10", netmask: "24", name: "vboxnet0"
        subconfig.vm.provider "virtualbox" do |vb|
            vb.customize ["modifyvm", :id, "--nictrace2", "on"]
            vb.customize ["modifyvm", :id, "--nictracefile2", "/Users/ahassany/repos/pmacct_lab/r1_peeringnetwork.pcap"]
            vb.customize ["modifyvm", :id, "--nictrace4", "on"]
            vb.customize ["modifyvm", :id, "--nictracefile4", "/Users/ahassany/repos/pmacct_lab/r1_dev.pcap"]
        end
        subconfig.vm.provision "ansible" do |ansible|
            ansible.playbook="ansible/r1.yml"
        end
    end

    config.vm.define "r11" do |subconfig|
        subconfig.vm.box = "ubuntu/focal64"
        subconfig.vm.hostname = "r11"
        subconfig.vm.network :private_network,  ip: "172.16.1.11", netmask: "24", virtualbox__intnet: "r1network"
        subconfig.vm.network :private_network,  ip: "172.16.11.10", netmask: "24", virtualbox__intnet: "r11network"
        subconfig.vm.provider "virtualbox" do |vb|
            vb.customize ["modifyvm", :id, "--nictrace2", "on"]
            vb.customize ["modifyvm", :id, "--nictracefile2", "/Users/ahassany/repos/pmacct_lab/r11_peeringnetwork.pcap"]
        end
        subconfig.vm.provision "ansible" do |ansible|
            ansible.playbook="ansible/r1.yml"
        end
    end


    config.vm.define "r2" do |subconfig|
        subconfig.vm.box = "ubuntu/focal64"
        subconfig.vm.hostname = "r2"
        subconfig.vm.network :private_network,  ip: "172.16.0.20", netmask: "24", virtualbox__intnet: "peeringnetwork"
        subconfig.vm.network :private_network,  ip: "172.16.2.10", netmask: "24", virtualbox__intnet: "r2network"
        subconfig.vm.provider "virtualbox" do |vb|
            vb.customize ["modifyvm", :id, "--nictrace2", "on"]
            vb.customize ["modifyvm", :id, "--nictracefile2", "/Users/ahassany/repos/pmacct_lab/r2_peeringnetwork.pcap"]
        end
        subconfig.vm.provision "ansible" do |ansible|
            ansible.playbook="ansible/r1.yml"
        end
    end

    config.vm.define "r3" do |subconfig|
        subconfig.vm.box = "ubuntu/focal64"
        subconfig.vm.hostname = "r3"
        subconfig.vm.network :private_network,  ip: "172.16.0.30", netmask: "24", virtualbox__intnet: "peeringnetwork"
        subconfig.vm.network :private_network,  ip: "172.16.3.10", netmask: "24", virtualbox__intnet: "r2network"
        subconfig.vm.provider "virtualbox" do |vb|
            vb.customize ["modifyvm", :id, "--nictrace2", "on"]
            vb.customize ["modifyvm", :id, "--nictracefile2", "/Users/ahassany/repos/pmacct_lab/r3_peeringnetwork.pcap"]
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
            vb.customize ["modifyvm", :id, "--nictracefile2", "/Users/ahassany/repos/pmacct_lab/pmacct_peeringnetwork.pcap"]
        end
        subconfig.vm.provision "ansible" do |ansible|
            ansible.playbook="ansible/pmacct.yml"
        end
    end
end
