Vagrant.configure("2") do |config|
  config.vm.hostname = "app" # Nombre VM
  config.vm.box = "ubuntu/trusty64" # Usar template descargado de Ubuntu
  config.vm.box_version = "20180404.0.0" # Version del template de Ubuntu
  config.vm.provision :shell do |shell|
      shell.inline = <<-SHELL
        sudo apt-get -y install python python-pip python-yaml
        sudo pip install --upgrade pip
        ##sudo pip install 'docker_py==1.10.6'
        sudo pip install docker-compose
      SHELL
  end
  config.vm.provision "ansible_local" do |ansible| # Utilizar ansible como provisioner local
    ansible.playbook = "playbook.yml" # Path al playbook de Ansible para instalar Docker
    ansible.install_mode = "pip" # Instalar ansible en la VM con pip
    #ansible.version = "2.5.0"  # Version de ansible a instalar
  end
  #config.vm.provision :shell do |shell|
   #   shell.inline = <<-SHELL
    #    sudo pip install docker-py
     # SHELL
    #end
  config.vm.network :forwarded_port, guest: 80, host: 8080 ## Port FOrwarding de la VM (80) a host local (8080)
end
