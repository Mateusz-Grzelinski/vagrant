# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-20.04"
  # config.vm.guest = :linux
  # config.vm.box = "generic/alpine315"

  # sometimes ceftificate provider might not be resolved by DNS
  # config.vm.box_download_insecure = true

  config.vm.provider "hyperv" do |hv|
    hv.vmname = "hyperv-vagrant-ansible-demo-vm-ubuntu"
    hv.cpus = "2"
    hv.memory = "2048"
    # hv.enable_enhanced_session_mode = true
  end

  # config.vm.provision "shell", inline: "ls"
  # config.vm.synced_folder ".", "/vagrant", :extra => "ro", create: true, owner: "vagrant", group: "vagrant"

  config.vm.provision "ansible_local" do |ansible|
    ansible.galaxy_role_file = "ansible/requirements.yml"
    ansible.galaxy_roles_path = "/etc/ansible/roles"
    ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path}"
    ansible.playbook = "ansible/playbooks/install_tools.yaml"
  end

  config.vm.provision "ansible_local" do |ansible|
    # ansible.become = true
    ansible.playbook = "ansible/playbooks/clone_roles.yaml"
    # ansible.limit = "all"
  end

  # config.vm.box_check_update = false
end
