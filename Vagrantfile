# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  if (/cygwin|mswin|mingw|bccwin|wince|emx/ =~ RUBY_PLATFORM) != nil
    config.vm.synced_folder ".", "/vagrant", mount_options: ["dmode=700,fmode=600"]
  else
    config.vm.synced_folder ".", "/vagrant"
  end 
  config.vm.define "ubunu-pptp-desktop" do |d|
    d.vm.box = "bento/ubuntu-16.04"
    d.vm.hostname = "ubunu-pptp-desktop"
    d.vm.network "public_network", bridge: "eno4", ip: "192.168.57.18", auto_config: "false", netmask: "255.255.255.0" , gateway: "192.168.57.1"
    default_router = "192.168.57.1"
    d.vm.provision :shell, inline: "ip route delete default 2>&1 >/dev/null || true; ip route add default via #{default_router}"
    d.vm.provider "virtualbox" do |v|
      v.memory = 4096
      v.cpus=2
    end
  end   
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end
  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
    config.vbguest.no_install = false
    config.vbguest.no_remote = false
  end
end
