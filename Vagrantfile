Vagrant.configure("2") do |config|

  if Vagrant.has_plugin?("vagrant-hostmanager")
    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
  end

  # ===================== db01 =====================
  config.vm.define "db01" do |machine|
    machine.vm.box = "centos/stream9"
    machine.vm.network "private_network", ip: "192.168.56.15"
    machine.vm.hostname = "db01"
    machine.vm.provider "virtualbox" do |vb|
      vb.name = "db01"
      vb.cpus = 2
      vb.memory = 2048
    end

    machine.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbooks/install_mariadb.yml"
      ansible.inventory_path = "inventory/hosts.ini"
      ansible.become = true
    end
  end

  # ===================== mc01 =====================
  config.vm.define "mc01" do |machine|
    machine.vm.box = "centos/stream9"
    machine.vm.network "private_network", ip: "192.168.56.14"
    machine.vm.hostname = "mc01"
    machine.vm.provider "virtualbox" do |vb|
      vb.name = "mc01"
      vb.cpus = 2
      vb.memory = 900
    end

    machine.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbooks/install_memchached.yml"
      ansible.inventory_path = "inventory/hosts.ini"
      ansible.become = true
    end
  end

  # ===================== rmq01 =====================
  config.vm.define "rmq01" do |machine|
    machine.vm.box = "centos/stream9"
    machine.vm.network "private_network", ip: "192.168.56.13"
    machine.vm.hostname = "rmq01"
    machine.vm.provider "virtualbox" do |vb|
      vb.name = "rmq01"
      vb.cpus = 2
      vb.memory = 600
    end

    machine.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbooks/install_rabbitmq.yml"
      ansible.inventory_path = "inventory/hosts.ini"
      ansible.become = true
    end
  end

  # ===================== app01 =====================
  config.vm.define "app01" do |machine|
    machine.vm.box = "centos/stream9"
    machine.vm.network "private_network", ip: "192.168.56.12"
    machine.vm.hostname = "app01"
    machine.vm.provider "virtualbox" do |vb|
      vb.name = "app01"
      vb.cpus = 2
      vb.memory = 4200
    end

    machine.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbooks/install_tomcat.yml"
      ansible.inventory_path = "inventory/hosts.ini"
      ansible.become = true
    end
  end

  # ===================== web01 =====================
  config.vm.define "web01" do |machine|
    machine.vm.box = "centos/stream9"
    machine.vm.network "private_network", ip: "192.168.56.11"
    machine.vm.hostname = "web01"
    machine.vm.provider "virtualbox" do |vb|
      vb.name = "web01"
      vb.cpus = 2
      vb.memory = 800
    end

    machine.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbooks/install_nginx.yml"
      ansible.inventory_path = "inventory/hosts.ini"
      ansible.become = true
    end
  end

end
