# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version  ">= 1.8  "
# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # config.vm.box = "centos/8"
  config.vm.box = "bento/amazonlinux-2"


  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  config.vm.network "forwarded_port", guest: 8080, host: 18080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

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
  config.vm.provider "virtualbox" do |vb|
    vb.name = "jenkins"
  # Display the VirtualBox GUI when booting the machine
    vb.gui = false
  #   # Customize the amount of memory on the VM:
    vb.memory = "2048"
    vb.cpus = 1
    vb.check_guest_additions = false
  end

  # Easy update
  config.vm.provision "shell", inline: <<-SHELL
    # sudo dnf -y install epel-release
    # sudo dnf repolist
    sudo yum -y update
    sudo amazon-linux-extras install python3.8
    sudo amazon-linux-extras install ruby2.6
    sudo amazon-linux-extras install docker
    sudo amazon-linux-extras install ansible2
    sudo amazon-linux-extras install java-openjdk11
  SHELL

  config.vm.provision "ansible_local" do |ansible|
    ansible.extra_vars = { :the_user => ENV['THE_USER'], :the_password => ENV['THE_PASSWORD']  }
    ansible.playbook = "base.yml"
    ansible.verbose = true
  end


  config.vm.provision "ansible_local" do |ansible|
    ansible.extra_vars = { :the_user => ENV['THE_USER'], :jenkins_username => ENV['JENKINS_USERNAME'], :jenkins_password => ENV['JENKINS_PASSWORD']  }
    ansible.become = true
    ansible.galaxy_role_file = "ansible_requirements.yml"
    ansible.galaxy_roles_path = "/etc/ansible/roles"
    ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"

    ansible.playbook = "jenkins.yml"
    ansible.verbose = false
  end
  config.vm.provision "shell", inline: <<-SHELL2
    sudo yum -y update
  SHELL2
end
