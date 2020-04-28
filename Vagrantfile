# -*- mode: ruby -*-
# vi: set ft=ruby :

$commonscript = <<-SCRIPT
yum update
yum -y install epel-release
yum -y install python-pip python-devel gcc vim git
python -m pip install --upgrade pip
SCRIPT

ENV["LANG"] = "en_US.UTF-8"
ENV["LC_ALL"] = "en_US.UTF-8"


Vagrant.configure("2") do |config|
  
    config.vm.box = "centos/7"
    
    config.vm.define "master" do |master|
        master.vm.network "private_network", ip: "192.168.33.10"
        master.vm.hostname = "master"
        
        master.vm.provider "virtualbox" do |vb|
            vb.name = "master-machine"
            vb.gui = false
            vb.cpus = 2
            vb.memory = "1536"
        end

        master.vm.provision "shell", inline: $commonscript
    end

    NodeCount = 1

    (1..NodeCount).each do |i|
      config.vm.define "node-#{i}" do |node|
        node.vm.network "private_network", ip: "192.168.33.2#{i}"
        node.vm.hostname = "node-#{i}"
        
        node.vm.provider "virtualbox" do |vb|
            vb.name = "node-#{i}"
            vb.gui = false
            vb.cpus = 2
            vb.memory = "1536"
        end

        node.vm.provision "shell", inline: $commonscript
      end
    end
end
