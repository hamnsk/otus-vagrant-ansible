ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/22.04"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 1
    vb.gui = false
  end

# Nginx balancer ip: 192.168.1.xxx
  config.vm.define "nginx1" do |nginx|
    nginx.vm.host_name = "nginx1"
#     nginx.vm.network "forwarded_port", guest: 80, host: 8080
    nginx.vm.network "private_network", ip: "192.168.32.10"
    nginx.vm.network "public_network", bridge: "en9: Display", ip: "192.168.1.70"
    nginx.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "balancer.yaml"
        ansible.inventory_path = "inventory/dev"
    end
  end

# Web App
  config.vm.define "app" do |app|
    app.vm.host_name = "app"
    app.vm.network "private_network", ip: "192.168.32.11"
    app.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "app.yaml"
        ansible.inventory_path = "inventory/dev"
    end
  end

vagrant_synced_folder_default_type = ""

end

