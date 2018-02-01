# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure("2") do |config|
  config.vm.define "vagrant-logtrade"

  config.vm.box = "debian/stretch64"

  config.vm.hostname = "logtrade.vagrant"
  config.vm.network :forwarded_port, guest: 22, host: 22255, id: 'ssh'
  config.vm.network :forwarded_port, guest: 5601, host: 23255, id: 'kibana'
  config.vm.network :forwarded_port, guest: 9200, host: 24255, id: 'elastic'


  config.vm.synced_folder ".", "/vagrant"
  config.ssh.port = 22255
  config.ssh.insert_key = false

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "10.10.10.2"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  config.ssh.forward_agent = true

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.

  config.vm.provider :virtualbox do |vb|
    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", "4096"]
    vb.customize ["modifyvm", :id, "--cpus",   "2"]
  end

# Left as a reminder for production
#  config.vm.provision "shell" do |s|
#    s.inline = "sudo swapoff -a"
#  end

  config.vm.provision "shell" do |s|
    s.inline = "sudo apt-get update"
  end

  config.vm.provision "shell" do |s|
    s.inline = "sudo apt-get install -y -q python python-pip git"
  end

  config.vm.provision "shell" do |s|
    s.inline = "sudo pip install pip --upgrade"
  end

  config.vm.provision "shell" do |s|
    s.inline = "sudo pip install ansible"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.host_key_checking = false
    ansible.playbook = "deploy-es-vagrant.yaml"
    ansible.tags = ENV['VAGRANT_TAGS']
    ansible.extra_vars = JSON.load(ENV['VAGRANT_EXTRA_VARS'])
    ansible.verbose = 'v'
  end
end
