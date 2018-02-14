# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.provider "virtualbox" do |v|
    v.memory = 512
    v.cpus = 2
  end

  config.vm.define "app" do |app|
    #app.vm.network :public_network, bridge: 'eth0'
    app.vm.hostname = "app.dev"
    app.vm.network :private_network, ip: '172.18.0.4'
  #  config.vm.provision "shell", path: "script.sh"
    app.vm.synced_folder ".", "/vagrant", disabled: true
    app.vm.synced_folder "shared_home/", "/shared_home",
        :owner => "confluence",
        :group => "confluence"
    app.vm.provision "shell", privileged: false, inline: <<-EOF
      if [ ! -f /home/vagrant/.ssh/id_rsa.pub ]; then
        wget --no-check-certificate https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant.pub -O /home/vagrant/.ssh/id_rsa.pub
        cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
      fi
    EOF
  end

  config.vm.define "app2" do |app|
    #app.vm.network :public_network, bridge: 'eth0'
    app.vm.hostname = "app2.dev"
    app.vm.network :private_network, ip: '172.18.0.5'
  #  config.vm.provision "shell", path: "script.sh"
    app.vm.synced_folder ".", "/vagrant", disabled: true
#    app.vm.synced_folder "shared_home/", "/shared_home"
    app.vm.provision "shell", privileged: false, inline: <<-EOF
      if [ ! -f /home/vagrant/.ssh/id_rsa.pub ]; then
        wget --no-check-certificate https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant.pub -O /home/vagrant/.ssh/id_rsa.pub
        cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
      fi
    EOF
  end

  config.vm.define "db" do |app|
    #app.vm.network :public_network, bridge: 'eth0'
    app.vm.hostname = "db.dev"
    app.vm.network :private_network, ip: '172.18.0.6'
  #  config.vm.provision "shell", path: "script.sh"
    app.vm.synced_folder ".", "/vagrant", disabled: true
    app.vm.provision "shell", privileged: false, inline: <<-EOF
      if [ ! -f /home/vagrant/.ssh/id_rsa.pub ]; then
        wget --no-check-certificate https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant.pub -O /home/vagrant/.ssh/id_rsa.pub
        cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
      fi
    EOF
  end

  config.vm.define "app3" do |app|
    #app.vm.network :public_network, bridge: 'eth0'
    app.vm.hostname = "app3.dev"
    app.vm.network :private_network, ip: '172.18.0.7'
  #  config.vm.provision "shell", path: "script.sh"
    app.vm.synced_folder ".", "/vagrant", disabled: true
    app.vm.synced_folder "shared_home/", "/shared_home",
        :owner => "confluence",
        :group => "confluence"
    app.vm.provision "shell", privileged: false, inline: <<-EOF
      if [ ! -f /home/vagrant/.ssh/id_rsa.pub ]; then
        wget --no-check-certificate https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant.pub -O /home/vagrant/.ssh/id_rsa.pub
        cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
      fi
    EOF
  end

  config.vm.define "controller" do |controller|
    controller.vm.network :private_network, ip: "172.18.0.3"
    controller.vm.hostname = "controller"
    # install ansible
    controller.vm.provision "shell", privileged: false, path: "install_ansible.sh"
    # run ansible
    controller.vm.provision "shell", privileged: false, inline: <<-EOF
      if [ ! -f /home/vagrant/.ssh/id_rsa ]; then
        wget --no-check-certificate https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant -O /home/vagrant/.ssh/id_rsa
#        wget --no-check-certificate https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant.pub -O /home/vagrant/.ssh/id_rsa.pub
        chmod 600 /home/vagrant/.ssh/id_*
      fi
      rm -rf /tmp/provisioning
      cp -r /vagrant/provisioning /tmp/provisioning
      cd /tmp/provisioning
      chmod -x hosts
      export ANSIBLE_HOST_KEY_CHECKING=False
#      ansible-playbook playbook.yml --inventory-file=hosts
    EOF
  end
end

#  config.vm.provision "ansible" do |ansible|
#    ansible.playbook = "apache.yml"
#  end

#config.vm.network "private
# _network", ip: "192.168.50.4",
  #  virtualbox__intnet: true

  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.


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
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
