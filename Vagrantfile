
Vagrant.configure("2") do |config|

  config.vm.define "bamboo" do |bamboo|
    bamboo.vm.network "private_network", ip: "192.168.56.50"
    bamboo.vm.network "forwarded_port", guest: 8085, host: 8085
    bamboo.vm.hostname = "bamboo"
    privileged = true
    bamboo.vm.provision "ansible" do |ansible|
        ansible.playbook = "bamboo/bamboo-playbook.yml"
    end
  end

  config.vm.define "bamboo-postgres" do |postgres|
    postgres.vm.hostname = "postgresql" 
    postgres.vm.network "private_network", ip: "192.168.56.51"
    postgres.vm.network "forwarded_port", guest: 5432, host: 5432, host_ip: "127.0.0.1"
    privileged = true
    postgres.vm.provision "ansible" do |ansible|
        ansible.playbook = "postgres/postgres.yml"
    end
  end

  config.vm.define "bamboo-worker" do |bamboo|
    bamboo.vm.network "private_network", ip: "192.168.56.52"
    bamboo.vm.hostname = "bamboo-worker"
    privileged = true
    bamboo.vm.provision "ansible" do |ansible|
        ansible.playbook = "bamboo/bamboo-worker.yml"
    end
  end

end 
