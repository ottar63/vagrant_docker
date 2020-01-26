# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do | config |
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.define "master" do | master |
    master.vm.box = "ubuntu/bionic64"
    master.vm.network "private_network", ip: "192.168.33.30"
    master.vm.hostname = "master"
    master.persistent_storage.enabled = true
    master.persistent_storage.location="/export/vagrant_db.vdi"
    master.persistent_storage.size = 10000
    master.persistent_storage.mountname="prosqldb"
    master.persistent_storage.filesystem = 'ext4'
    master.persistent_storage.mountpoint = "/data/prosqldb"
    master.persistent_storage.volgroupname = "volumegrp1"
    master.persistent_storage.diskdevice = '/dev/sdc'
    master.vm.provider "virtualbox" do |vb|
    #   # Customize the amount of memory on the VM:
      vb.memory = "512"
      
      # Create persistent volume
      #file_to_disk='/export/vagrant_db.vdi'
      #if ! File.exist?(file_to_disk)
      #  vb.customize ['createhd','--filename',file_to_disk,'--size', 50 * 1024]
      #end
      #vb.customize ['storageattach',:id,'--storagectl','SCSI','--port',2,'--device',0,'--type', 'hdd','--medium','/export/vagrant_db.vdi']
    end
  end
  config.vm.define "node1" do|node1|
    node1.vm.box = "ubuntu/bionic64"
    node1.vm.network "private_network", ip:"192.168.33.31"
    node1.vm.hostname = "node1"
    node1.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
    end
  end
  config.vm.define "node2" do|node2|
    node2.vm.box = "ubuntu/bionic64"
    node2.vm.network "private_network", ip:"192.168.33.32"
    node2.vm.hostname = "node2"
    node2.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
    end
  end
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
  end

end

