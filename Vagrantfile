# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|
	# Installing Ubuntu 12.04, 64 bit
	config.vm.box = "ubuntu1204"
	config.vm.box_url = "http://files.vagrantup.com/precise32.box"

	# Setup networking
	config.vm.host_name = "donaldtrunk.dev"
	config.vm.network :hostonly, "99.99.99.99"

	# Sharing the nginx-default folder
	config.vm.share_folder "default", "/var/www/nginx-default", "~/Sites", :nfs => true

	# Using Chef Solo for provisioning
	config.vm.provision :chef_solo do |chef|

		# Define the path to the cookbooks folder
		chef.cookbooks_path = "cookbooks"

		# Define node data for use in recipes
		chef.json = {
			:mysql => {
				:server_debian_password => 'root',
				:server_root_password   => 'root',
				:server_repl_password   => 'root'
			}
		}

		# Add the recipes to install
		chef.add_recipe "apt"
		chef.add_recipe "git"
		chef.add_recipe "curl"
		chef.add_recipe "php"
		chef.add_recipe "nginx"
		chef.add_recipe "mysql::server"
		chef.add_recipe "wp-cli"
		# chef.add_recipe "wordpress"
	end
end