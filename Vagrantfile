# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Base VM OS configuration.
  config.vm.box = "geerlingguy/rockylinux8"
  config.vm.box_check_update = false
  config.ssh.insert_key = false
  config.vm.synced_folder '.', '/vagrant', disabled: true
  # Do not automatically update the guest ddtitions
  config.vbguest.auto_update = false if Vagrant.has_plugin?("vagrant-vbguest")

  # MySQL.
  config.vm.define "db1" do |db1|
    db1.vm.hostname = "db1.test"
    db1.vm.network :private_network, ip: "192.168.2.5"
  end

  # MySQL.
  config.vm.define "db2" do |db2|
    db2.vm.hostname = "db2.test"
    db2.vm.network :private_network, ip: "192.168.2.6"

    # Run Ansible provisioner once for all VMs at the end.
    db2.vm.provision "ansible" do |ansible|
      ansible.playbook = "configure.yml"
      ansible.inventory_path = "inventories/vagrant/inventory.ini"
      ansible.limit = "all"
      ansible.extra_vars = {
        ansible_user: 'vagrant',
        ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
      }
     end
  end
end
