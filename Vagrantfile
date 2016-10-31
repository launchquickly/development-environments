# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/wily64"
  
  config.vm.hostname = 'default.launchquickly.com'
  config.vm.network :private_network, ip: '192.168.50.50'

  # Share additional folders to the guest VM.
  # Code
  config.vm.synced_folder "../src", "/usr/local/src", create: true, type: "nfs"
  # Puppet environment
  config.vm.synced_folder "../lq_control_repo/", "/etc/puppetlabs/code/environments/lq_control_repo/", create: true
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
     wget https://apt.puppetlabs.com/puppetlabs-release-pc1-wily.deb
     sudo dpkg -i puppetlabs-release-pc1-wily.deb
     sudo apt-get update
     sudo apt-get install -y puppet-agent
     
     cat <<EOT >> /etc/puppetlabs/puppet/puppet.conf
[main]
environment = lq_control_repo
EOT

  SHELL

  config.vm.provision "shell", inline: <<-SHELL
     echo -e '#{File.read("#{Dir.home}/.gitconfig")}' > '/home/vagrant/.gitconfig'
  SHELL
  
   # vagrant-r10k plugin configuration
  config.r10k.puppet_dir      = '../lq_control_repo/'
  config.r10k.puppetfile_path = '../lq_control_repo/Puppetfile'
  config.r10k.module_path     = "../lq_control_repo/modules"
  
  config.vm.provision "puppet" do |puppet|
  
    puppet.environment_path = ".."
    puppet.environment = 'lq_control_repo'

    puppet.module_path    = ["../lq_control_repo/modules", "../lq_control_repo/site"]

    puppet.options = "--verbose --debug "

  end

  # Set up SSH agent forwarding for git amongst others.
  config.ssh.forward_agent = true

end
