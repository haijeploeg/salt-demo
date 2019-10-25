# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version.
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  centos_box = "bento/centos-7"
  net_ip = "192.168.50"

  config.vm.define :master, primary: true do |master_config|
    master_config.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = 1
    end

    master_config.vm.box = "#{centos_box}"
    master_config.vm.host_name = "saltmaster.local"
    master_config.vm.network "private_network", ip: "#{net_ip}.10"
    master_config.vm.synced_folder ".", "/vagrant", disabled: true
    master_config.vm.synced_folder "states/", "/srv/states", type: "virtualbox"
    master_config.vm.synced_folder "pillar/", "/srv/pillar", type: "virtualbox"

    master_config.vm.provision :salt do |salt|
      salt.master_config = "config/master"
      salt.minion_config = "config/minion"
      salt.install_type = "stable"
      salt.install_master = true
      salt.no_minion = false
      salt.verbose = true
      salt.colorize = true
      salt.bootstrap_options = "-P -c /tmp"
    end
  end

  [
    ["minion1", "#{net_ip}.11", "1024", centos_box],
    ["minion2", "#{net_ip}.12", "1024", centos_box],
  ].each do |vmname,ip,mem,os|
    config.vm.define "#{vmname}" do |minion_config|
      minion_config.vm.provider "virtualbox" do |vb|
        vb.memory = "#{mem}"
        vb.cpus = 1
      end

      minion_config.vm.box = "#{os}"
      minion_config.vm.hostname = "#{vmname}.local"
      minion_config.vm.network "private_network", ip: "#{ip}"
      minion_config.vm.synced_folder ".", "/vagrant", disabled: true

      minion_config.vm.provision :salt do |salt|
        salt.minion_config = "config/minion"
        salt.install_type = "stable"
        salt.verbose = true
        salt.colorize = true
        salt.bootstrap_options = "-P -c /tmp"
      end
    end
  end
end