# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "bento/ubuntu-18.04"
  config.vm.network :forwarded_port, guest: 80, host: 80
  config.vm.network :forwarded_port, guest: 3306, host: 3306
  config.vm.synced_folder ".", "/var/www/"
  config.vm.hostname = "ubuntu"

  # For the running docker-compose automaticaly
  config.vm.provision :docker
  config.vm.provision :docker_compose, yml: "/var/www/docker/docker-compose.yml", rebuild: true, run: "always"

  # We are going to give VM 1/4 system memory & access to all cpu cores on the host
  config.vm.provider "virtualbox" do |vb|
    host = RbConfig::CONFIG['host_os']
    if host =~ /darwin/
      cpus = `sysctl -n hw.ncpu`.to_i
      mem = `sysctl -n hw.memsize`.to_i / 1024 / 1024 / 4
    elsif host =~ /linux/
      cpus = `nproc`.to_i
      mem = `grep 'MemTotal' /proc/meminfo | sed -e 's/MemTotal://' -e 's/ kB//'`.to_i / 1024 / 4
    else
      cpus = 2
      mem = 1024
    end
    vb.customize ["modifyvm", :id, "--memory", mem]
    vb.customize ["modifyvm", :id, "--cpus", cpus]
  end

   config.vm.provision "shell", inline: <<-SHELL
    # Install docker and docker compose
    sudo -i
    echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections
    curl -sSL https://get.docker.com/ | sh
    usermod -aG docker vagrant
    curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose
  SHELL
end
