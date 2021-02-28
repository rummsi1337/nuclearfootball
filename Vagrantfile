# -*- mode: ruby -*-
# vi: set ft=ruby :

# Temporary workaround to Python bug in macOS High Sierra which can break Ansible
# https://github.com/ansible/ansible/issues/34056#issuecomment-352862252
# This is an ugly hack tightly bound to the internals of Vagrant.Util.Subprocess, specifically
# the jailbreak method, self-described as "quite possibly, the saddest function in all of Vagrant."
# That in turn makes this assignment the saddest line in all of Vagrantfiles.
ENV["VAGRANT_OLD_ENV_OBJC_DISABLE_INITIALIZE_FORK_SAFETY"] = "YES"

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/groovy64"

  config.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = "4"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "main.yaml"
    ansible.vault_password_file = "vault_pass"
    ansible.verbose = "vv"
  end

end
