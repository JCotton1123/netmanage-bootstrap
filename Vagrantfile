VAGRANTFILE_API_VERSION = "2"

box             = 'xcezx/centos6.5-with-ansible'
hostname        = 'netmanage2.local'
ram             = '768'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = box
  config.vm.host_name = hostname
#  config.vm.network "private_network"
  config.vm.network "public_network"
#  config.vm.network "public_network", ip: "192.168.7.3"

  config.vm.provider "virtualbox" do |v|
    v.name = hostname
  end

  config.vm.provision "ansible" do |ansible|
    ansible.extra_vars = {
      ansible_ssh_user: 'vagrant',
    }
    ansible.sudo = true
    ansible.groups = {
      "app-server" => ["default"],
      "db-server" => ["default"],
      "all_groups:children" => ["app-server", "db-server"]
    }
    ansible.playbook = "site.yml"
  end
end
