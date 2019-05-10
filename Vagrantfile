# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "centos/7"

  config.vm.network "private_network", ip: "192.168.33.10"

  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end

  # if Vagrant.has_plugin?("vagrant-vbguest")
  #   config.vbguest.auto_update = false
  # end
  config.vm.synced_folder ".", "/vagrant", type:"virtualbox"

  # プロビジョニング実行
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "/vagrant/site.yml"
  end

end
