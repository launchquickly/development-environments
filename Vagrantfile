# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/wily64"
  
  config.vm.network :private_network, ip: '192.168.50.50'

  # Share additional folders to the guest VM.
  # Code
  config.vm.synced_folder "../src", "/usr/local/src", create: true, type: "nfs"
  # Maven repository
  config.vm.synced_folder "../maven/repository", "/home/vagrant/.m2/repository", create: true, type: "nfs"
  # Eclipse preferences
  config.vm.synced_folder "config/eclipse", "/home/vagrant/config/eclipse", create: true, type: "nfs"
  # SSH directory mount
  config.vm.synced_folder "~/.ssh", "/home/vagrant/config/.ssh", create: true, type: "nfs"
  # Disable vagrant folder
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider "virtualbox" do |vb|
     # Display the VirtualBox GUI when booting the machine
     vb.gui = true

     vb.memory = "8192"

     vb.cpus = 2
     vb.customize ["modifyvm", :id, "--ioapic", "on"]

     # this line enables communication over host VPN connection by guest
     vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
     vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.provision "shell", inline: <<-SHELL
     sudo apt-get update
  SHELL

  config.vm.provision "shell", inline: <<-SHELL
     echo -e '#{File.read("#{Dir.home}/.gitconfig")}' > '/home/vagrant/.gitconfig'
  SHELL

  # Set up SSH agent forwarding for git amongst others.
  config.ssh.forward_agent = true

end
