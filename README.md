https://github.com/opscode-cookbooks/runit/pull/23/files


To add something new (like redis):
====================================
* Modify Cheffile
	* cookbook 'redis', :git => 'https://github.com/ctrabold/chef-redis.git'
* Download dependencies
	* librarian-chef install
* Update node (vagrant.json) runlist
	* add "recipe[redis]"