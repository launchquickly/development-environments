# Java Development Environment

Vagrant based development environment for developing Java

## Pre-requisites

- [Virtualbox](https://www.virtualbox.org/) 5.1.x or above is installed
- [Vagrant](https://www.vagrantup.com/) 1.9.x or above is installed
- Vagrant plugin [vboxguest](https://github.com/dotless-de/vagrant-vbguest) is installed
- [lq_control_repo](https://github.com/launchquickly/lq_control_repo) is checked out in same directory as root development-environments directory
- ~/.gitconfig is present as this will be mapped into guest


## Set-up

- Ubuntu 16.10
- Puppet Agent
- Git
- Open JDK 8
- Maven 3.3.9
- Gradle 4.0.1
- Spring Tool Suite IDE 3.9.0

## Directories mapped from guest

- /home/vagrant/dev/src is mapped from ~/dev/src
- /home/vagrant/config/.ssh is mapped from ~/.ssh
- /etc/puppetlabs/code/environments/lq_control_repo is mapped from ../../lq_control_repo
