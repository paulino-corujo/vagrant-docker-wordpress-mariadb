# -*- mode: ruby -*-
# vi: set ft=ruby :

unless Vagrant.has_plugin?("vagrant-docker-compose")
  system("vagrant plugin install vagrant-docker-compose")
  puts "Dependencies installed, please try the command again."
  exit
end

CHECK_PUBLIC_KEY = File.join("#{Dir.home}/.ssh/id_rsa.pub")

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "private_network", ip: "10.5.10.5"
  config.vm.synced_folder "wordpress", "/var/www/html", create: true, mount_options: ["dmode=777,fmode=664"]

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
    v.name = "wordpress"
  end

  if File.exist?(CHECK_PUBLIC_KEY)
    config.vm.provision "shell" do |s|
      ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
        echo "#{ssh_pub_key}" >> /home/vagrant/.ssh/authorized_keys
        echo "#{ssh_pub_key}" >> /root/.ssh/authorized_keys
      SHELL
    end
  end

  config.vm.provision "docker"
  config.vm.provision :docker_compose, yml: "/vagrant/docker-compose.yml", rebuild: true, project_name: "wordpress", run: "always"
end
