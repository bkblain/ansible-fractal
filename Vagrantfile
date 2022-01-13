# -*- mode: ruby -*-
# vi: set ft=ruby :

# For a complete reference, please see the online documentation at
# https://docs.vagrantup.com.

# Every Vagrant development environment requires a box. You can search for
# boxes at https://vagrantcloud.com/search.

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/impish64"
  # config.vm.box = "fedora/35-cloud-base"

  # config.vm.provision "ansible" do |ansible|
  #   ansible.become = true
  #   ansible.playbook = "playbooks/ubuntu2004-playbook-cis_level1_server.yml"

    # ansible.playbook = "playbooks/fedora-playbook-ospp.yml"

    # Skipping tags
    # 
    # sudo_require_authentication: because the STIG will remove NOPASSWD
    # preventing the Vagrant user from logging in without a password
  #   ansible.skip_tags = "sudo_require_authentication"
  # end

  config.vm.provision "ansible" do |ansible|
    ansible.become = true
    ansible.playbook = "oscap-scan.yml"
  #   ansible.verbose = "vvv"
  end


  # sudo aide --config /etc/aide/aide.conf --check
end
