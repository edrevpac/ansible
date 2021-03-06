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

#system("ssh-keygen -f ~/.ssh/id_rsa -t rsa -N ''")

system("
    if [ #{ARGV[0]} = 'up' ]; then
        echo 'How about a new key? If YES, you will need to add it to GitHub for everything else to work!'
        ssh-keygen -f ~/.ssh/id_rsa -t rsa -N ''
    fi
")


Vagrant.configure(2) do |config|

  config.ssh.insert_key = false
  config.vm.provider "virtualbox" do |v|
    v.memory = 512
    v.cpus = 1
  end

  config.vm.define "jenkins" do |web|
	   web.vm.box = "bento/debian-9.1-i386"
     web.vm.hostname = "jenkins"
#	   web.vm.network "public_network"
	   web.vm.network "private_network", ip: "192.168.56.196"
  end

  config.vm.define "tomcat" do |app|
	   app.vm.box = "bento/debian-9.1-i386"
     app.vm.hostname = "tomcat"
#	   app.vm.network "public_network"
	   app.vm.network "private_network", ip: "192.168.56.197"
  end

#  config.vm.provision "shell", inline: "ssh-keygen -f ~/.ssh/id_rsa -t rsa -N ''"
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playlist.yml"
#    ansible.verbose = "v"
    ansible.host_vars = {
      "jenkins" => {
        "ansible_ssh_host" => "192.168.56.196",
        "ansible_ssh_port" => 22,
        "ansible_ssh_user" => 'vagrant',
        "ansible_ssh_private_key_file" => "~/.ssh/id_rsa"
        },
      "tomcat" => {
        "ansible_ssh_host" => "192.168.56.197",
        "ansible_ssh_port" => 22,
        "ansible_ssh_user" => 'vagrant',
        "ansible_ssh_private_key_file" => "~/.ssh/id_rsa"
        }
    }
  end

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
