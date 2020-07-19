# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
echo I am provisioning...
date > /etc/vagrant_provisioned_at
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.hostname = "postgresql"
  config.vm.network :private_network, ip: "192.168.60.4"
  config.vm.synced_folder ".", "/home/vagrant/", disabled: true

  config.vm.provision "shell", inline: $script
  config.vm.provision :shell, :path => "Vagrant-setup/bootstrap.sh"

  # PostgreSQL Server port forwarding
  config.vm.network "forwarded_port", guest: 5432, host: 15432
end
