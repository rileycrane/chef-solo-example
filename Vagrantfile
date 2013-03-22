# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'rubygems'
require 'bundler'

#Bundler.require
require 'multi_json'

Vagrant::Config.run do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "precise64tutorial"
  config.vm.forward_port 80, 8085

  VAGRANT_JSON = MultiJson.load(Pathname(__FILE__).dirname.join('nodes', 'vagrant.json').read)
  config.vm.provision :chef_solo do |chef|
       chef.cookbooks_path = ["site-cookbooks", "cookbooks"]
       chef.roles_path = "roles"
       chef.data_bags_path = "data_bags"
       chef.provisioning_path = "/tmp/vagrant-chef"

       # You may also specify custom JSON attributes:
       chef.json = VAGRANT_JSON
       VAGRANT_JSON['run_list'].each do |recipe|
        chef.add_role(recipe)
       end if VAGRANT_JSON['run_list']

       Dir["#{Pathname(__FILE__).dirname.join('roles')}/*.json"].each do |role|
        chef.add_role(role)
       end
  end
    
end
