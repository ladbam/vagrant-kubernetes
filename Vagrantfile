IMAGE_NAME = "bento/ubuntu-16.04"
N = 2

Vagrant.configure("2") do |config|
      config.vm.provision "shell", inline: <<-SHELL
          apt-get update
          echo "192.168.55.10  master-node" >> /etc/hosts
          echo "192.168.55.11  worker-node1" >> /etc/hosts
          echo "192.168.55.12  worker-node2" >> /etc/hosts
      SHELL
      
      config.vm.define "kube-master" do |master|
        master.vm.box = "bento/ubuntu-16.04"
        master.vm.hostname = "kube-master-node"
        master.vm.network "private_network", ip: "192.168.55.10"
        master.vm.provider "virtualbox" do |vb|
            vb.memory = 4048
            vb.cpus = 2
        end
        master.vm.provision "shell", path: "scripts/kube.sh"
        master.vm.provision "shell", path: "scripts/master.sh"
      end
  
      (1..N).each do |i|
    
      config.vm.define "node0#{i}" do |node|
        node.vm.box = "bento/ubuntu-16.04"
        node.vm.hostname = "kube-worker-node#{i}"
        node.vm.network "private_network", ip: "192.168.55.1#{i}"
        node.vm.provider "virtualbox" do |vb|
            vb.memory = 2048
            vb.cpus = 1
        end
        node.vm.provision "shell", path: "scripts/kube.sh"
        node.vm.provision "shell", path: "scripts/node.sh"
      end
      
      end
    end
