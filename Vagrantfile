# coding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "debian/jessie64"

  config.vm.define :consul1 do |consul1_config|
    consul1_config.vm.hostname = "consul1"
    consul1_config.vm.network "private_network", ip:"192.168.100.10"
    consul1_config.vm.provider :virtualbox do |vb|
      vb.memory = 256
      vb.cpus = 1
    end
  end

  config.vm.define :consul2 do |consul2_config|
    consul2_config.vm.hostname = "consul2"
    consul2_config.vm.network "private_network", ip:"192.168.100.11"
    consul2_config.vm.provider :virtualbox do |vb|
      vb.memory = 256
      vb.cpus = 1
    end
  end

  config.vm.define :consul3 do |consul3_config|
    consul3_config.vm.hostname = "consul3"
    consul3_config.vm.network "private_network", ip:"192.168.100.12"
    consul3_config.vm.provider :virtualbox do |vb|
      vb.memory = 256
      vb.cpus = 1
    end
  end

  config.vm.define :java1 do |java1_config|
    java1_config.vm.hostname = "java1"
    java1_config.vm.network "private_network", ip:"192.168.100.20"
    java1_config.vm.provider :virtualbox do |vb|
      vb.memory = 512
      vb.cpus = 1
    end
  end

  config.vm.define :java2 do |java2_config|
    java2_config.vm.hostname = "java2"
    java2_config.vm.network "private_network", ip:"192.168.100.21"
    java2_config.vm.provider :virtualbox do |vb|
      vb.memory = 512
      vb.cpus = 1
    end
  end

  # Cache APT
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end


  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "play.yml"
  end
end

