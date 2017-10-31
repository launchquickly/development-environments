# Hugo Development Environment

Vagrant based development environment for developing static websites using [Hugo](https://gohugo.io/)

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
- Hugo 0.30.2

## Directories mapped from guest

- /home/vagrant/dev/src is mapped from ~/dev/src
- /home/vagrant/config/.ssh is mapped from ~/.ssh
- /etc/puppetlabs/code/environments/lq_control_repo is mapped from ../../lq_control_repo
