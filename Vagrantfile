# -*- mode: ruby -*-
# vi: set ft=ruby :

#require 'yaml'
#cfg = YAML::load_file("config.yml")

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"


Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  config.vm.box = "chef/centos-6.6"
  #config.vm.box = "puppetlabs/ubuntu-14.04-64-puppet"
  #config.vm.box = "baremettle/centos-6.5"
    
  config.vm.provision :shell, :path => "scripts/common.sh"
  config.vm.provision :shell, :path => "scripts/puppet.sh"
  config.vm.provision :shell, :path => "scripts/puppet-modules.sh"


  config.vm.provision "puppet" do |puppet|
      puppet.hiera_config_path= "puppet/hiera.yaml"
      puppet.working_directory = "/tmp/vagrant-puppet/"
      puppet.manifests_path = "puppet/manifests"
      puppet.module_path = "puppet/modules"
      #puppet.options = "--verbose --debug"
      puppet.options = "--verbose"
  end

  config.vm.define "server", autostart: true do |host|
      #host.vm.network "private_network", ip: "192.168.34.120"
      config.vm.network "forwarded_port", guest: 80, host: 8080
      host.vm.hostname = "server.test.lvo"
  end
  config.vm.define "proxy", autostart: false do |host|
      #host.vm.network "private_network", ip: "192.168.34.121"
      host.vm.hostname = "proxy.test.lvo"
  end

#  config.vm.synced_folder '.', '/vagrant', type: 'nfs'
  #config.vm.synced_folder '.', '/vagrant', type: 'rsync'

end
