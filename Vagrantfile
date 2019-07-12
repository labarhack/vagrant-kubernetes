# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX_NAME = ENV['BOX_NAME'] || "labarhack/kubernetes_20190712.0"
KUBE_NODE_COUNT= ENV['KUBE_NODE_COUNT'] || 1
$kube_master_addr = "10.10.10.50"

Vagrant.configure("2") do |config|

  config.vm.box = BOX_NAME
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
  end


  # ---------------------------------------------------
  # Kubernetes Master (api, scheduler, controller)
  # ---------------------------------------------------
  config.vm.define "kube_master_1" do |kube_master_1|
    kube_master_1.vm.hostname = "kube-master-1"
    kube_master_1.vm.network "private_network", ip: $kube_master_addr
    kube_master_1.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/kube_master.yml"
        ansible.become = true
        ansible.compatibility_mode = "2.0"
        ansible.verbose = true
        ansible.extra_vars = {
          node_addr: $kube_master_addr
        } 
    end
  end

  # ---------------------------------------------------
  # Kubernetes Worker
  # ---------------------------------------------------
  (1..KUBE_NODE_COUNT).each do |machine_id|
    config.vm.define "kube_node_#{machine_id}" do |kube_node|
      kube_node.vm.hostname = "kube-node-#{machine_id}"
      kube_node.vm.network "private_network", ip: "10.10.10.6#{machine_id}"
      if machine_id == 1
        kube_node.vm.network "forwarded_port", guest: 80, host: "8081", guest_ip: "10.10.10.6#{machine_id}"
        kube_node.vm.network "forwarded_port", guest: 8080, host: "8080", guest_ip: "10.10.10.6#{machine_id}"
      end
      kube_node.vm.provision "ansible" do |ansible|
          ansible.playbook = "ansible/kube_node.yml"
          ansible.become = true
          ansible.compatibility_mode = "2.0"
          ansible.verbose = true
          ansible.extra_vars = {
            node_addr: "10.10.10.6#{machine_id}",
          } 
      end
    end
  end
end
