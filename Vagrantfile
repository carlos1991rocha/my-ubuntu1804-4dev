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
  config.vm.box = "felipecassiors/ubuntu1804-4dev"

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
  config.vm.synced_folder "~/Repository", "/home/vagrant/Repository"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|

    # Display the VirtualBox GUI when booting the machine
    vb.gui = true

    # Set the display name of the VM in VirtualBox
    vb.name = "my-bionic-4dev"

    # Customize the amount of memory on the VM:
    vb.memory = "8192"
    # Customize the amount of CPU on the VM:
    vb.cpus = "2"

    # Make the DNS calls be resolved on host
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]

  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    set -ex

    export DEBIAN_FRONTEND=noninteractive
    sudo apt-get update
    sudo apt-get dist-upgrade -qq

    sudo snap refresh

    # Set keyboard layout to Portuguese (Brazil)
    gsettings set org.gnome.desktop.input-sources sources "[('xkb', 'br')]"

    # Set timezone to America/Sao_Paulo
    sudo rm /etc/localtime && sudo ln -s /usr/share/zoneinfo/America/Sao_Paulo  /etc/localtime

    # Turn off blank screen
    gsettings set org.gnome.desktop.session idle-delay 0

    # Enable login shell
    profile="$(gsettings get org.gnome.Terminal.ProfilesList default)"
    profile="${profile:1:-1}" # remove leading and trailing single quotes
    gsettings set "org.gnome.Terminal.Legacy.Profile:/org/gnome/terminal/legacy/profiles:/:$profile/" login-shell true

    #!/bin/bash

  SCHEMA="org.gnome.shell"
  KEY="favorite-apps"
  TO_ADD_VALUE="google-chrome.desktop"

  STATUS=$(gsettings get ${SCHEMA} ${KEY})

  # Optional proof, whether value to add already exsists
  if [[ $STATUS == *"'$TO_ADD_VALUE'"* ]]; then
      echo "$TO_ADD_VALUE is already in the list!"
  else
      gsettings set ${SCHEMA} ${KEY} "['$TO_ADD_VALUE',${STATUS#*[}"
      echo "Added $TO_ADD_VALUE to the list."
  fi

  SCHEMA="org.gnome.shell"
  KEY="favorite-apps"
  TO_ADD_VALUE="code_code.desktop"

  STATUS=$(gsettings get ${SCHEMA} ${KEY})

  # Optional proof, whether value to add already exsists
  if [[ $STATUS == *"'$TO_ADD_VALUE'"* ]]; then
      echo "$TO_ADD_VALUE is already in the list!"
  else
      gsettings set ${SCHEMA} ${KEY} "['$TO_ADD_VALUE',${STATUS#*[}"
      echo "Added $TO_ADD_VALUE to the list."
  fi

  SCHEMA="org.gnome.shell"
  KEY="favorite-apps"
  TO_ADD_VALUE="postman_postman.desktop"

  STATUS=$(gsettings get ${SCHEMA} ${KEY})

  # Optional proof, whether value to add already exsists
  if [[ $STATUS == *"'$TO_ADD_VALUE'"* ]]; then
      echo "$TO_ADD_VALUE is already in the list!"
  else
      gsettings set ${SCHEMA} ${KEY} "['$TO_ADD_VALUE',${STATUS#*[}"
      echo "Added $TO_ADD_VALUE to the list."
  fi

  SCHEMA="org.gnome.shell"
  KEY="favorite-apps"
  TO_ADD_VALUE="gnome-terminal.desktop"

  STATUS=$(gsettings get ${SCHEMA} ${KEY})

  # Optional proof, whether value to add already exsists
  if [[ $STATUS == *"'$TO_ADD_VALUE'"* ]]; then
      echo "$TO_ADD_VALUE is already in the list!"
  else
      gsettings set ${SCHEMA} ${KEY} "['$TO_ADD_VALUE',${STATUS#*[}"
      echo "Added $TO_ADD_VALUE to the list."
  fi

  SHELL
end
