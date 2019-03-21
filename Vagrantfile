# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.define "Server01" do |srv01|
    srv01.vm.box = "bento/ubuntu-16.04"
	srv01.vm.provider "virtualbox" do |vb|
	  vb.memory = "1024"  
	end
    srv01.vm.hostname = "srv01"
    srv01.vm.network "private_network", ip: "192.168.55.100"
    # MySQL Port nur im Private Network sichtbar
	# db.vm.network "forwarded_port", guest:3306, host:3306, auto_correct: false 
		srv01.vm.provision "shell", inline: <<-SHELL
		sudo apt-get update
		sudo apt-get -y install apache2
		sudo ufw allow 'Apache'
		sudo mkdir /var/www/webdav
		sudo chown www-data.www-data /var/www/webdav
		sudo a2enmod dav
		sudo a2enmod dav_fs
		sudo a2ensite webdav
		sudo systemctl restart apache2
		
SHELL
	end
   
  config.vm.define "Client" do |cl01|
    cl01.vm.box = "ubuntu/xenial64"
    cl01.vm.hostname = "cl01"
    cl01.vm.network "private_network", ip:"192.168.55.101" 
	cl01.vm.provider "virtualbox" do |vb|
	  vb.memory = "1024"  
	end      
	cl01.vm.provision "shell", inline: <<-SHELL
		sudo apt-get update
SHELL
	end  
 end
