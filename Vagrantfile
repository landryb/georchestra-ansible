# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "debian/jessie64"

  # set CPU and RAM
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--cpus", "1"]
  end

  # Create a public network, which generally matches to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  config.vm.network :public_network
  config.vm.network "forwarded_port", guest: 5432, host: 5432

  # Give a nice name ("georchestra") to the VM:
  config.vm.define "georchestra" do |georchestra|
  end

  config.vm.provision "ansible" do |ansible|
    # execute this playbook for vm provisioning:
    ansible.playbook = "playbooks/georchestra.yml"
    # display ansible-playbook output:
    ansible.verbose = "v"
    # limit ansible-playbook execution to one machine:
    ansible.limit = "mygeorchestra"
    # ... as referenced in our "hosts" file:
    ansible.inventory_path = "hosts"
  end

end
