# -*- mode: ruby -*-
# vi: set ft=ruby :
$k8s_instances = 1
$vm_ip_addr_start = 170
#$bridge = "usb0" #name of network interface with internet connection 
$bridge = "wlp2s0" #name of network interface with internet connection 
$vm_cidr = "192.168.0" # virtual machines CIDR
Vagrant.configure("2") do |config|
    config.vm.box = "generic/ubuntu2204"
    config.vm.box_check_update = false
    (1..$k8s_instances).each do |i|
        config.vm.define "control-node-#{i}" do |node|
            node.vm.network "public_network", ip: "#{$vm_cidr}.#{$vm_ip_addr_start+i}", bridge: $bridge
            node.vm.hostname = "control-node-#{i}"
            node.vm.provider "virtualbox" do |vb|
                vb.gui = false
                vb.memory = "8192"
                vb.cpus=4
            end
        end
    end
end