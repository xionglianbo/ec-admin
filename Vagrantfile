# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false

  config.vm.box = "juwai-centos68"
  config.vm.box_url = "http://downloads.juwai.io/devops/boxes/juwai-centos68.box"

  config.vm.network :private_network, ip: "192.168.111.3"
  config.vm.network "forwarded_port", guest: 6003, host: 6003

  host = RbConfig::CONFIG['host_os']

  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
  end

  config.vm.provider "virtualbox" do |v|
    # access to all cpu cores on the host
    if host =~ /darwin/
      cpus = `sysctl -n hw.ncpu`.to_i
    elsif host =~ /linux/
      cpus = `nproc`.to_i
    else
      cpus = 2
    end

    v.customize ["modifyvm", :id, "--memory", 1024]
    v.customize ["modifyvm", :id, "--cpus", cpus]

    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

end
