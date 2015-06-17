# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "hashicorp/precise64"

  config.vm.network "forwarded_port", guest: 80, host: 8080  # apache
  config.vm.network "forwarded_port", guest: 8000, host: 8000  # django dev
  config.vm.network "forwarded_port", guest: 3306, host: 8306  # mysql

  config.vm.provider "virtualbox" do |vb|
    # i'm being pretty generous about the memory and cpus here 
    # because neither my computer, nor the server is very limited
    # in resources.
    vb.cpus = "4"
    vb.memory = "4000"
  end

  config.vm.synced_folder "thewulf/", "/home/mwinter80/thewulf.org/thewulf"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provision/playbook.yml"
  end
end
