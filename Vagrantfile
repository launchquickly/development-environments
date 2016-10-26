# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "boxcutter/ubuntu1604-desktop"

  # Share additional folders to the guest VM.
  # Code
  config.vm.synced_folder "../../src", "/usr/local/src", create: true
  # Maven repository
  config.vm.synced_folder "../../maven/repository", "/home/vagrant/.m2/repository", create: true
  # Eclipse preferences
  config.vm.synced_folder "config/eclipse", "/home/vagrant/config/eclipse", create: true
  # SSH directory mount
  config.vm.synced_folder "~/.ssh", "/home/vagrant/config/.ssh", create: true
  # Disable vagrant folder
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider "virtualbox" do |vb|
     # Display the VirtualBox GUI when booting the machine
     vb.gui = true

     # Customize the amount of memory on the VM:
     vb.memory = "8192"

     # this line enables communication over host VPN connection by guest
     vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  config.vm.provision "shell", inline: <<-SHELL
     sudo apt-get update
  SHELL

  config.vm.provision "shell", inline: <<-SHELL
     echo -e '#{File.read("#{Dir.home}/.gitconfig")}' > '/home/vagrant/.gitconfig'
  SHELL

  # Ensure all files in home directory are owned by vagrant user
  config.vm.provision "shell", inline: <<-SHELL
     sudo chown -R vagrant:vagrant /home/vagrant
  SHELL

  # Set up SSH agent forwarding for git amongst others.
  config.ssh.forward_agent = true

end
