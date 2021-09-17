# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  config.ssh.insert_key = false

# This is the provisioning for the two Virtual Machines
  (1..2).each do |i|
   config.vm.define "web-#{i}" do |web|
     web.vm.box = "centos/7"
     web.vm.hostname = "web-#{i}"
     web.vm.network "private_network", ip: "192.168.33.1#{i}"
     web.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512", "--cpus", "1", "--name", "web-#{i}"]
     end
     web.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbooks/nginx/webserver.yml"
      ansible.groups = {
        "webservers" => ["web-#{i}"]
      }
    end
   end
  end

# This is the provisioning for the Database 
# Fow now this won't do anything, but soon it will :)
  config.vm.define "db" do |db|
   db.vm.box = "centos/7"
   db.vm.hostname = "db"
   db.vm.network "private_network", ip: "192.168.33.100"
   db.vm.provision "shell", inline: "echo Iam DB server"
  end
end

