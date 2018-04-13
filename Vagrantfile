Vagrant.configure("2") do |config|
  config.vm.hostname = "app" # Nombre de la VM
  config.vm.box = "ubuntu/trusty64" # Usar template para Ubuntu 14.04 descargado del catálogo de Vagrant
  config.vm.box_version = "20180404.0.0" # Version del template de Ubuntu
  config.vm.provision :shell do |shell| # Instalar dependencias de docker y usar comandos integrados de shell contra la VM
      shell.inline = <<-SHELL
        sudo apt-get -y install python-pip
        sudo pip install --ignore-installed six
        sudo pip install docker-compose
      SHELL
  end
  config.vm.provision "ansible_local" do |ansible| # Usar Ansible como un aprovisionador local
    ansible.playbook = "playbook.yml" # Ruta al Ansible-playbook para instalar Docker
    #ansible.install_mode = "pip" # Opcional: instalar Ansible en la VM usando pip
    #ansible.version = "2.5.0"  # Opcional: elegir version específica de Ansible a instalar
  end
  config.vm.network :forwarded_port, guest: 80, host: 8080 ## Port Forwarding desde la VM (80) al localhost (8080)
end