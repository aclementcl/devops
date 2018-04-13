Vagrant.configure("2") do |config|
  config.vm.hostname = "app" # VM Name
  config.vm.box = "ubuntu/trusty64" # Use template for Ubuntu 14.04 downloaded from Vagrant Catalog
  config.vm.box_version = "20180404.0.0" # Ubuntu template version
  config.vm.provision :shell do |shell| # Install docker dependencies and use shell inline commands against the VM
      shell.inline = <<-SHELL
        sudo apt-get -y install python-pip
        sudo pip install --ignore-installed six
        sudo pip install docker-compose
      SHELL
  end
  config.vm.provision "ansible_local" do |ansible| # Use Ansible as a plocal provisioner
    ansible.playbook = "playbook.yml" # Path to the Ansible Playbook to install Docker
    ansible.install_mode = "pip" # Install Ansible on the VM with pip
    #ansible.version = "2.5.0"  # Choose Ansible specified version
  end
  config.vm.network :forwarded_port, guest: 80, host: 8080 ## Port Forwarding from VM (80) to local host (8080)
end