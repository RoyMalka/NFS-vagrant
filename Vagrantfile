# -*- mode: ruby -*-
# vi: set ft=ruby :

box_base = "bento/ubuntu-14.04"
box_cpu_count = 1
box_ram_mb = "1024"
nfs_ip = "192.168.77.14"


$script = <<SCRIPT
sudo apt-get update
sudo apt-get install nfs-kernel-server -y
mkdir -p /shared
sudo chmod 777 /shared
echo "/shared *(rw,fsid=0,insecure,no_subtree_check,sync)" | sudo tee -a /etc/exports
sudo service nfs-kernel-server restart
SCRIPT




Vagrant.configure("2") do |config|

  config.vm.box = box_base
  config.vm.provision "shell", inline: $script
  
  config.vm.provider "virtualbox" do |vb|
    vb.cpus = box_cpu_count
    vb.memory = box_ram_mb
  end
  
  config.vm.define "NFS-server", primary: true do |nfs|
    nfs.vm.hostname = "NFS-server"
    nfs.vm.network "private_network", ip: nfs_ip


end
end
