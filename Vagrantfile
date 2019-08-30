# -*- mode: ruby -*-
# vi: set ft=ruby :

unless Vagrant.has_plugin?("vagrant-docker-compose")
  system("vagrant plugin install vagrant-docker-compose")
  puts "Dependencies installed, please try the command again."
  exit
end

Vagrant.configure("2") do |config|
  port = 8080
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "forwarded_port", guest: port, host: port, ip: "127.0.0.1"
  config.vm.network "forwarded_port", guest: 8081, host: 8081, ip: "127.0.0.1"
  config.vm.network "forwarded_port", guest: 3306, host: 3306
  config.vm.network "public_network"

  config.vm.synced_folder ".", "/vagrant"
  config.vm.synced_folder "./www", "/vagrant/www"
  config.vm.synced_folder "./data", "/vagrant/data"

  config.vm.provision :shell, inline: "apt-get update"
  
  config.vm.provision :docker
  # config.vm.provision :docker_compose, yml: "/vagrant/docker-compose.yml", run: "always"
  config.vm.provision :shell, path: "docker.sh"
end