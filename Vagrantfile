# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|

  # VM settings
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  # config.vm.boot_mode = :gui
 
  # Network settings 
  config.vm.host_name = "lamp"
  config.vm.network :hostonly, "192.168.56.20"
  config.vm.forward_port 80, 8080
  config.vm.share_folder "www", "/var/www", "www"

  # Set the Timezone to something useful
  config.vm.provision :shell, :inline => "echo \"Europe/London\" | sudo tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata"

  # Update the server
  config.vm.provision :shell, :inline => "apt-get update --fix-missing"

  # Enable provisioning with chef solo
  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"
    chef.add_recipe "apt"
    chef.add_recipe "openssl"
    chef.add_recipe "apache2"
    chef.add_recipe "mysql"
    chef.add_recipe "mysql::server"
    chef.add_recipe "php"
    chef.add_recipe "php::module_apc"
    chef.add_recipe "php::module_curl"
    chef.add_recipe "php::module_mysql"
    chef.add_recipe "php::module_mcrypt"
    chef.add_recipe "apache2::mod_php5"
    chef.add_recipe "apache2::mod_rewrite"
    chef.add_recipe "git"
    chef.add_recipe "composer"
    chef.json = {
        :mysql => {
            :server_root_password => 'root',
            :bind_address => '127.0.0.1'
        }
    } 
  end

end
