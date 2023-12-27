BOX = "bento/ubuntu-22.04"

Vagrant.configure("2") do |config|

  if `uname -m`.strip == "aarch64"
    config.vm.box = BOX + "-arm64"
  else
    config.vm.box = BOX
  end
  config.vm.box_check_update = true

  config.vm.define "bamboo" do |bamboo|
    bamboo.vm.network "private_network", ip: "192.168.56.50"
    bamboo.vm.network "forwarded_port", guest: 8085, host: 8085
    bamboo.vm.hostname = "bamboo"
    bamboo.vm.provider "virtualbox" do |vb|
      vb.cpus = 1
      vb.memory = 2048
    end
    privileged = true
    bamboo.vm.provision "ansible" do |ansible|
        ansible.playbook = "bamboo/bamboo-playbook.yml"
    end
  end

  config.vm.define "bamboo-postgres" do |postgres|
    postgres.vm.hostname = "postgresql" 
    postgres.vm.network "private_network", ip: "192.168.56.51"
    postgres.vm.network "forwarded_port", guest: 5432, host: 5432, host_ip: "127.0.0.1"
    postgres.vm.provider "virtualbox" do |vb|
      vb.cpus = 1
      vb.memory = 2048
    end
    privileged = true
    postgres.vm.provision "ansible" do |ansible|
        ansible.playbook = "postgres/postgres.yml"
    end
  end

  config.vm.define "bamboo-worker" do |bambooworker|
    bambooworker.vm.network "private_network", ip: "192.168.56.52"
    bambooworker.vm.hostname = "bamboo-worker"
    bambooworker.vm.provider "virtualbox" do |vb|
      vb.cpus = 2
      vb.memory = 4096
    end
    privileged = true
    bambooworker.vm.provision "ansible" do |ansible|
        ansible.playbook = "bamboo/bamboo-worker.yml"
    end
  end

end 
