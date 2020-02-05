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
  config.vm.define "vamaster" do | vamaster |
    vamaster.vm.box = "ubuntu/bionic64"
    vamaster.vm.network "private_network", ip: "192.168.33.30"
    vamaster.vm.hostname = "vamaster"
    vamaster.persistent_storage.enabled = true
    vamaster.persistent_storage.location="/export/vagrant_db.vdi"
    vamaster.persistent_storage.size = 10000
    vamaster.persistent_storage.mountname="prosqldb"
    vamaster.persistent_storage.filesystem = 'ext4'
    vamaster.persistent_storage.mountpoint = "/data/prosqldb"
    vamaster.persistent_storage.volgroupname = "volumegrp1"
    vamaster.persistent_storage.diskdevice = '/dev/sdc'
    vamaster.vm.provider "virtualbox" do |vb|
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
  config.vm.define "vanode1" do|vanode1|
    vanode1.vm.box = "ubuntu/bionic64"
    vanode1.vm.network "private_network", ip:"192.168.33.31"
    vanode1.vm.hostname = "vanode1"
    vanode1.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
    end
  end
  config.vm.define "vanode2" do|vanode2|
    vanode2.vm.box = "ubuntu/bionic64"
    vanode2.vm.network "private_network", ip:"192.168.33.32"
    vanode2.vm.hostname = "vanode2"
    vanode2.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
    end
  end
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
  end

end

