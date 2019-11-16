# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  config.ssh.insert_key = true
  config.vm.box = "kzielins/ubuntu-16.04-amd64"
  #config.vm.box = "bento/ubuntu-18.04"

  config.vm.define "eduroam" do |my|
	my.vm.network "public_network"
	my.vm.network :forwarded_port, guest: 22, host: 2244, id: 'ssh'
	# This helps with testing, but shouldn't be used in production
	my.vm.synced_folder ".", "/vagrant"
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "site.yml"
    ansible.inventory_path = "inventories/development"
    ansible.limit = 'eduroam'
  end
end
