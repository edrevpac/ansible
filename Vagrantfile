# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  # config.vm.box = "ubuntu/trusty64"

Vagrant.configure(2) do |config|

#  config.vm.boot_timeout = 300
  config.ssh.insert_key = false
#  config.ssh.private_key_path = "~/.ssh/id_rsa"
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 1
  end

  config.vm.define "test" do |yo|
	yo.vm.box = "bento/debian-9.1-i386"
  yo.vm.hostname = "test"
	yo.vm.network "public_network"
	yo.vm.network "private_network", ip: "192.168.56.195"
	yo.vm.network "forwarded_port", guest: 80, host: 5050
  end

  config.vm.define "jenkins" do |web|
	web.vm.box = "bento/debian-9.1-i386"
  web.vm.hostname = "jenkins"
	web.vm.network "public_network"
	web.vm.network "private_network", ip: "192.168.56.196"
	web.vm.network "forwarded_port", guest: 80, host: 6060
#    config.vm.provision "ansible" do |ansi_2|
#    ansi_2.verbose = "v"
#    ansi_2.playbook = "install_jenkins.yml"
#    end
#  web.vm.provision "shell", inline: 
#  U=jenkins P="Jenkins001"; adduser $U; echo $P | passwd $U --stdin 
#  useradd -u jenkins -g users -d /home/jenkins -s /bin/bash -p $(echo Jenkins001 | openssl passwd -1 -stdin) jenkins
  end

  config.vm.define "tomcat" do |app|
	app.vm.box = "bento/debian-9.1-i386"
  app.vm.hostname = "tomcat"
	app.vm.network "public_network"
	app.vm.network "private_network", ip: "192.168.56.197"
	app.vm.network "forwarded_port", guest: 80, host: 7070
#    config.vm.provision "ansible" do |ansi_1|
#    ansi_1.verbose = "v"
#    ansi_1.playbook = "install_tomcat.yml"
#    end
  end

#  config.vm.provision "shell", inline: "ssh-keygen -f ~/.ssh/id_rsa -t rsa -N ''"
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
#  config.vm.provision "ansible" do |ansible|
#    ansible.playbook = "~/Documents/git/ansible/playlist.yml"
#    ansible.host_vars = {
#      "test" => {
#        "ansible_host" => "192.168.56.195",
#        "ansible_port" => 22,
#        "ansible_user" => "vagrant"
#        },
#      "jenkins" => {
#        "ansible_host" => "192.168.56.196",
#        "ansible_port" => 22,
#        "ansible_user" => "vagrant"
#        },
#      "tomcat" => {
#        "ansible_host" => "192.168.56.197",
#        "ansible_port" => 22,
#        "ansible_user" => "vagrant"
#        }
#    }
#  end

end

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = true

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.56.101"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo apt-get update
  #   sudo apt-get install -y apache2
  # SHELL
