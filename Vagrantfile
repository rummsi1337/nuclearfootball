# -*- mode: ruby -*-
# vi: set ft=ruby :

# Temporary workaround to Python bug in macOS High Sierra which can break Ansible
# https://github.com/ansible/ansible/issues/34056#issuecomment-352862252
# This is an ugly hack tightly bound to the internals of Vagrant.Util.Subprocess, specifically
# the jailbreak method, self-described as "quite possibly, the saddest function in all of Vagrant."
# That in turn makes this assignment the saddest line in all of Vagrantfiles.
ENV["VAGRANT_OLD_ENV_OBJC_DISABLE_INITIALIZE_FORK_SAFETY"] = "YES"

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.vm.box = "ubuntu/groovy64"

  boxes = [
    { :name => "kube1", :ip => "192.168.77.2" },
    { :name => "kube2", :ip => "192.168.77.3" },
    { :name => "kube3", :ip => "192.168.77.4" },
    { :name => "kube4", :ip => "192.168.77.5" }
  ]

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"
    vb.cpus = "1"
  end

  boxes.each_with_index do |opts, index|
    config.vm.define opts[:name] do |config|
      config.vm.hostname = opts[:name]
      config.vm.network :private_network, ip: opts[:ip]

      # Provision the VMs after last VM has been created.
      if index == boxes.size - 1
        config.vm.provision "ansible" do |ansible|
          ansible.playbook = "main.yaml"
          ansible.inventory_path = "vagrant_inventory.yaml"
          ansible.limit = "all"
          # ansible.tags = "raspi"
          ansible.verbose == "vv"
        end
      end
    end
  end

end
