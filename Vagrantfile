# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.provider :vmware_fusion do |provider, config|
    config.vm.box = "netsensia/ubuntu-trusty64"
    provider.vmx["memsize"] = "1024"
    provider.vmx["numvcpus"] = "2"
  end

  config.vm.provider :virtualbox do |provider|
    provider.customize ["modifyvm", :id, "--memory", 1024]
    provider.customize ["modifyvm", :id, "--cpus", 1]
    provider.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    provider.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.provision "shell", inline: <<-SCRIPT
    sudo apt-get install -y software-properties-common
    sudo apt-add-repository ppa:ansible/ansible
    sudo apt-get update
    sudo apt-get install -y ansible
  SCRIPT

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
  end
end
