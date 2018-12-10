
  #
  # -*- mode: ruby -*-
  # vi: set ft=ruby :

  # All Vagrant configuration is done below. The "2" in Vagrant.configure
  # configures the configuration version (we support older styles for
  # backwards compatibility). Please don't change it unless you know what
  # you're doing.
  Vagrant.configure("2") do |config|

    config.vm.box = "debian/stretch64"
    # config.vm.box = "debiankube"



    config.vm.provider "virtualbox" do |vb|
      vb.cpus = 2
      # Customize the amount of memory on the VM:
      vb.memory = "2048"
    end

    # config.vm.provision "shell", inline: <<-SHELL
    #     sudo apt-get -q update
    #     sudo apt-get -q -y upgrade
    #     sudo apt-get -q -y install apt-transport-https ca-certificates  curl  gnupg2  software-properties-common net-tools ipvsadm
    #     sudo curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
    #     sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
    #     sudo apt-get -q -y update
    #     sudo apt-get -q -y install docker-ce=17.09.1~ce-0~debian
    #     sudo usermod -aG docker vagrant
    #     sudo systemctl restart docker
    #   SHELL

    config.vm.define "kube_master" do |master|
      master.vm.hostname = "master"
      master.vm.network "private_network", ip: "192.168.50.11"
      master.vm.network "forwarded_port", guest: 6443, host: 6443

      master.vm.provision "ansible" do |ansible|
        ansible.inventory_path = "ansible/inventory"
        ansible.playbook = "ansible/playbook.yml"
        ansible.become = true
      end
    end

    config.vm.define "kube_worker-01" do |worker|
      worker.vm.hostname = "worker-01"
      worker.vm.network "private_network", ip: "192.168.50.21"

      worker.vm.provision "ansible" do |ansible|
        ansible.inventory_path = "ansible/inventory"
        ansible.playbook = "ansible/playbook.yml"
        ansible.become = true
      end

    end

    config.vm.define "kube_worker-02" do |worker|
      worker.vm.hostname = "worker-02"
      worker.vm.network "private_network", ip: "192.168.50.22"

      worker.vm.provision "ansible" do |ansible|
        ansible.inventory_path = "ansible/inventory"
        ansible.playbook = "ansible/playbook.yml"
        ansible.become = true
      end

    end

  end
