Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"

  # VM para o GitLab Runner
  config.vm.define "runner" do |runner|
    runner.vm.network "private_network", ip: "192.168.56.6"
    runner.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
    end
    runner.vm.provision "shell", privileged: false, path: "config_runner/install_docker.sh"
    runner.vm.provision "shell", privileged: false, path: "config_runner/install_runner.sh" 
    runner.vm.provision "shell", privileged: false, path: "config_runner/register_runner.sh"
  end  

  # VM para a aplicação
  config.vm.define "app" do |app|
    app.vm.network "private_network", ip: "192.168.56.8"
    app.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
    end
    # Provisionamento para instalar Python 3
    app.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y python3
    SHELL
  end

  # VM para o banco de dados
  config.vm.define "database" do |db|
    db.vm.network "private_network", ip: "192.168.56.10"
    db.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
    end
    # Provisionamento para instalar Python 3
    db.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y python3
    SHELL
  end
end
