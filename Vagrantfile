# check is necessary plugins are available
[
  { :name => "vagrant-guest_ansible", :version => ">= 0.0.3" },
].each do |plugin|

  if not Vagrant.has_plugin?(plugin[:name], plugin[:version])
    raise "#{plugin[:name]} #{plugin[:version]} is required. Please run `vagrant plugin install #{plugin[:name]}`"
  end
end

# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  provisioner = Vagrant::Util::Platform.windows? ? :guest_ansible : :ansible

  config.vm.network "private_network", ip: "192.168.19.46"
  
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
  end
  
  # Ansible provisioning.
  config.vm.provision provisioner do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.sudo = true
  end
end
