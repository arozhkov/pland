# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "c7"
  config.vm.box_url = "/home/arozhkov/Downloads/centos7.box"
  
  config.ssh.username = "vagrant"
  config.ssh.password = "vagrant"
  
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "private_network", type: "dhcp"

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
  config.vm.provision "shell", inline: <<-SHELL
   sudo yum update -y
   sudo yum install -y wget git net-tools bind-utils iptables-services bridge-utils bash-completion nc

   sudo bash -c "echo '172.28.128.10 master.kub' >> /etc/hosts"
   sudo bash -c "echo '172.28.128.11 node1.kub' >> /etc/hosts"
   sudo bash -c "echo '172.28.128.12 node2.kub' >> /etc/hosts"
   sudo bash -c "echo '172.28.128.13 node3.kub' >> /etc/hosts"

   cat /vagrant/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
  SHELL
  
  config.vm.define "master" do |master|
    master.vm.hostname = 'master.kub'
    master.vm.network "private_network", ip: "172.28.128.10"
  end

  config.vm.define "node1" do |node1|
    node1.vm.hostname = "node1.kub"
    node1.vm.network "private_network", ip: "172.28.128.11"
  end
  
  config.vm.define "node2" do |node2|
    node2.vm.hostname = "node2.kub"
    node2.vm.network "private_network", ip: "172.28.128.12"
  end
  
  config.vm.define "node3" do |node3|
    node3.vm.hostname = "node3.kub"
    node3.vm.network "private_network", ip: "172.28.128.13"
  end
  
  
end
