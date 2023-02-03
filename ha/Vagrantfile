# -*- mode: ruby -*-
# vi: set ft=ruby :
$k8s_control_node_num = 3
$k8s_worker_num = 3
$k8s_gw_num = 2
$bridge = "wlp2s0" #name of network interface with internet connection 
$vm_cidr = "192.168.0" # virtual machines CIDR
$vm_ip_addr_start = 130
Vagrant.configure("2") do |config|
    config.vm.box = "generic/ubuntu2204"
    config.vm.box_check_update = false
    (1..($k8s_control_node_num + $k8s_worker_num)).each do |i|
        if i < $k8s_control_node_num + 1
            config.vm.define "control-node-#{i}" do |node|
                node.vm.network "public_network", ip: "#{$vm_cidr}.#{$vm_ip_addr_start+i}", bridge: $bridge
                node.vm.hostname = "control-node-#{i}"
                node.vm.provider "virtualbox" do |vb|
                    vb.gui = false
                    vb.memory = "2048"
                    vb.cpus=2
                end
            end
        end
        if i > $k8s_control_node_num
            config.vm.define "worker-#{i-$k8s_worker_num}" do |node|
                node.vm.network "public_network", ip: "#{$vm_cidr}.#{$vm_ip_addr_start+i}", bridge: $bridge
                node.vm.hostname = "worker-#{i-$k8s_worker_num}"
                node.vm.provider "virtualbox" do |vb|
                    vb.gui = false
                    vb.memory = "8192"
                    vb.cpus = 2
                end
            end
        end
    end
    if $k8s_gw_num != 0
        (1..($k8s_gw_num)).each do |j|
            config.vm.define "gw-#{j}" do |gw|
                gw.vm.network "public_network", ip: "#{$vm_cidr}.#{$vm_ip_addr_start + $k8s_control_node_num + $k8s_worker_num+j}", bridge: $bridge
                gw.vm.hostname = "gw-#{j}"
                gw.vm.provider "virtualbox" do |vb|
                    vb.gui = false
                    vb.memory = "1024"
                    vb.cpus = 1
                end
            end
        end
    end
end