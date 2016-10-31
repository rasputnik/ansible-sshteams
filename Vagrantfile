# -*- mode: ruby -*-
# vi: set ft=ruby :

## if you change these, change vagrant_hosts too
#
# would _dearly_ love to make this less clunkable,
# and just read vagrant_hosts directly.

hosts = [
  {:name => "stub1",       :ip => "10.4.0.2", :ram => 400},
  {:name => "stub2",       :ip => "10.4.0.4", :ram => 400},
]

Vagrant.configure("2") do |config|

  # setup /etc/hosts on each vm
  # - requires the vagrant-hostmanager plugin
  config.hostmanager.enabled = true
  # set to 'false' if you don't wan't to manage _your_ /etc/hosts
  config.hostmanager.manage_host = true
  config.hostmanager.include_offline = true

  hosts.each do |host|
    config.vm.define host[:name] do |c|

      # same box for all hosts
      c.vm.box = "box-cutter/centos68"

      # stop Vagrant 'helping'
      c.ssh.insert_key = false

      c.vm.host_name = host[:name]
      c.vm.network :private_network, ip: host[:ip], netmask: "255.255.255.0"

      c.vm.provider("virtualbox") do |vb|
        vb.memory = host[:ram]
      end

      # turn off shared folder
      c.vm.synced_folder ".", "/vagrant", :disabled => true

    end
  end
end
