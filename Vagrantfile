# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
N = 3
Vagrant.configure(2) do |config|
  config.vm.box = "mrlesmithjr/trusty64"
  (1..N).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.hostname = "node#{i}"
      node.vm.network :private_network, ip: "192.168.202.20#{i}"
    end
    config.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
    end
    if i == N
      config.vm.provision "ansible" do |ansible|
        ansible.groups = {
          "zookeeper-nodes" => [
            "node1",
            "node2",
            "node3"
          ]
        }
        ansible.playbook = "playbook.yml"
      end
    end
  end
end
