# -*- mode: ruby -*-
# vi: set ft=ruby :
#

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

CEPH_NODES=10
IPSTART=10
CEPH_DISK_SIZE='50G'

Vagrant.configure("2") do |config|

   # For vagrant hostmanager plugin
   config.hostmanager.enabled = true
   config.hostmanager.manage_host = true
   config.hostmanager.ignore_private_ip = false
   config.vm.box = "base"

   # Image to use
   config.vm.box = "generic/ubuntu1604"
   config.vm.box_check_update = false

	# Creating the master nodes
	(1..CEPH_NODES).each do |i|
	  config.vm.define "ceph-#{i}" do |box|
	    box.vm.hostname = "ceph-#{i}"
	    box.vm.network :private_network, ip: "192.168.5.#{IPSTART + i}", :netmask => "255.255.255.0"
	    # box.vm.network :private_network, ip: "192.168.6.#{IPSTART + i}", :netmask => "255.255.255.0"
	    box.vm.provider :libvirt do |domain|
	      domain.memory = 2048
	      domain.cpus = 1
         domain.storage :file, :size => "#{CEPH_DISK_SIZE}" 
         domain.storage :file, :size => "#{CEPH_DISK_SIZE}" 
         domain.storage :file, :size => "#{CEPH_DISK_SIZE}" 
	    end
	  end
	end

end
