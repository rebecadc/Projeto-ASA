# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"
  config.ssh.insert_key = false

  config.vm.provider "virtualbox" do |vb|
    vb.linked_clone = true
    vb.check_guest_additions = false
  end

  config.vm.define "arq" do |arq|
    arq.vm.hostname = "arq.clara.rebeca.devops"
    arq.vm.network "private_network", ip: "192.168.56.121"

    arq.vm.provider "virtualbox" do |vb|
      vb.memory = 512
    end

    (0..2).each do |x|
      arq.vm.disk :disk, size: "10GB", name: "arq_disk-#{x}"
    end
  end

  config.vm.define "db" do |db|
    db.vm.hostname = "db.clara.rebeca.devops"
    db.vm.network "private_network", type: "dhcp"
    db.vm.provider "virtualbox" do |vb|
      vb.memory = 512
    end
  end

  config.vm.define "app" do |app|
    app.vm.hostname = "app.clara.rebeca.devops"
    app.vm.network "private_network", type: "dhcp"
    app.vm.provider "virtualbox" do |vb|
      vb.memory = 512
    end
  end

  config.vm.define "cli" do |cli|
    cli.vm.hostname = "cli.clara.rebeca.devops"
    cli.vm.network "private_network", type: "dhcp"
    cli.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
    end
  end
end

