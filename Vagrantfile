# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  # config.vm.box = "bento/ubuntu-20.04"
  config.vm.box = "centos/7"
  # provisioner = Vagrant::Util::Platform.windows? ? :guest_ansible : :ansible
  #config.ssh.username = "vagrant"
  #config.ssh.password = "vagrant"

 # if Vagrant.has_plugin?("vagrant-vbguest")
 #   config.vbguest.auto_update = false
 # end 

  Anz=2
  (1..Anz).each do | i |
    config.vm.define "target#{i}" do |target|
      target.vm.network "private_network", ip: "192.168.179.#{1+i}"
     # target.vm.network "forwarded_port", guest: 80, host: "880#{i}"
      target.vm.hostname = "VBoxVM#{i}"
      target.vm.provider "virtualbox" do |vb|
         vb.gui = true
         vb.check_guest_additions = false
         vb.memory = "2048"
         vb.cpus = 2
         vb.name = "VirtualBx#{i}"
        end
      target.vm.provision "shell", inline: <<-EOF
     # if [ ! -f /home/vagrant/.ssh/id_rsa ]; then
     #        wget --no-check-certificate https://raw.githubusercontent.com/hashicorp/vagrant/master/keys/vagrant -O /home/vagrant/.ssh/id_rsa
     #        wget --no-check-certificate https://raw.githubusercontent.com/hashicorp/vagrant/master/keys/vagrant.pub -O /home/vagrant/.ssh/id_rsa.pub
     #        chmod 600 /home/vagrant/.ssh/id_*
     # fi
        sudo yum update -y
        sudo yum install -y gcc
        cat id_ed25519.pub >> /home/vagrant/.ssh/authorized_keys
        mkdir -p /home/vagrant/hola
        cp /vagrant/Hola.c /home/vagrant/hola
        cd /home/vagrant/hola
        gcc -o hola Hola.c
        chmod 755 hola
        ./hola
      EOF


        # target.vm.provision "shell", privileged: false, path: "install_ansible.sh"
        # # run ansible
        # target.vm.provision "shell", privileged: false, inline: <<-EOF
        #   if [ ! -f /home/vagrant/.ssh/id_rsa ]; then
        #     wget --no-check-certificate https://raw.githubusercontent.com/hashicorp/vagrant/master/keys/vagrant -O /home/vagrant/.ssh/id_rsa
        #     wget --no-check-certificate https://raw.githubusercontent.com/hashicorp/vagrant/master/keys/vagrant.pub -O /home/vagrant/.ssh/id_rsa.pub
        #     chmod 600 /home/vagrant/.ssh/id_*
        #   fi
        #   rm -rf /tmp/provisioning
        #   cp -r /vagrant/provisioning /tmp/provisioning
        #   cd /tmp/provisioning
        #   chmod -x hosts
        #   export ANSIBLE_HOST_KEY_CHECKING=False
        #   ansible-playbook playbook.yml --inventory-file=hosts
        # EOF
       # target.vm.provision provisioner do |ansible|
       #   ansible.playbook = "playbook.yaml"
       # end

    end
  end
  
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"
  # config.vm.network "public_network", type: "dhcp"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Disable the default share of the current code directory. Doing this
  # provides improved isolation between the vagrant box and your host
  # by making sure your Vagrantfile isn't accessable to the vagrant box.
  # If you use this you may want to enable additional shared subfolders as
  # shown above.
  # config.vm.synced_folder ".", "/vagrant", disabled: true

  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
