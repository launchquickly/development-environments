# -*- mode: ruby -*-
# vi: set ft=ruby :

env_path = '/etc/puppetlabs/code/environments/lq_control_repo'
ctrl_repo = 'lq_control_repo'

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/wily64"
  
  config.vm.hostname = 'default.launchquickly.com'
  config.vm.network :private_network, ip: '192.168.50.50'

  # Share additional folders to the guest VM.
  # Code
  config.vm.synced_folder "../src", "/usr/local/src", create: true, type: "nfs"
  # Puppet environment
  config.vm.synced_folder "../#{ctrl_repo}", env_path, create: true
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
     dpkg -i puppetlabs-release-pc1-wily.deb
     apt-get update
     apt-get install -y puppet-agent
     
     rm -rf "#{env_path}/modules/*"
     
     /opt/puppetlabs/puppet/bin/gem install r10k
     /opt/puppetlabs/puppet/bin/r10k puppetfile install --puppetfile "#{env_path}/Puppetfile" --moduledir "#{env_path}/modules"
  SHELL

  config.vm.provision "shell", inline: <<-SHELL
     echo -e '#{File.read("#{Dir.home}/.gitconfig")}' > '/home/vagrant/.gitconfig'
  SHELL
  
  config.vm.provision "puppet" do |puppet|
  
    puppet.environment_path = ".."
    puppet.environment = ctrl_repo

    puppet.options = "--verbose --debug "

  end

  # Set up SSH agent forwarding for git amongst others.
  config.ssh.forward_agent = true

end
