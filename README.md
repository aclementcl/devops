#Devops-Challenge -- BETA VERSION

A quick deployment of a website using Vagrant+VirtualBox+Ansible+DockerCompose

##To get everything up & running:

1. Install Virtual Platform & Vagrant (if not installed already)
2. Clone devops-challenge git repo # git clone https://github.com/marcossv9/devops-challenge and place it on the directory you want to launch vagrant from.
3. Navigate to local repo directory & start vagrant ```# sudo vagrant up```
4. Enjoy

##If you want to do the whole thing manually follow this steps:

**Install VirtualBox**

Go to https://www.virtualbox.org/wiki/Linux_Downloads and download and install the version of VBOX for your OS.

In my case I download the file -> https://download.virtualbox.org/virtualbox/5.2.8/VirtualBox-5.2-5.2.8_121009_openSUSE132-1.x86_64.rpm

And installed it with the command:

- sudo zypper in VirtualBox-5.2-5.2.8_121009_openSUSE132-1.x86_64.rpm

**Install Vagrant**

Go to https://www.vagrantup.com/downloads.html and follow the steps to install Vagrant on your prefered OS.

In this case I use OpenSuseLEAP so the command is:

- sudo zypper in vagrant_2.0.3_x86_64rpm

**Create a directory where you are going to work with Vagrant

- mkdir Vagrant-Project
- cd Vagrant-Project

**Init Vagrant to generate a Vagrantfile in the current directory**

- vagrant init

**Edit the Vagrantfile to define a VM with Docker Engine and Docker-compose. Then it will execute a local Ansible-playbook to start two Docker Containers inside the VM using Docker Compose**

Here is the Vagrant file with comments to understand each line of the file:

https://github.com/marcossv9/devops-challenge/blob/master/Vagrantfile 

**Create two Dockerfiles that will be executed by Docker Compose and the run a website and a proxy server**

Create a docker compose folder where you are going to host two Dokerfiles for the web server and proxy server. Use the command:

- mkdir compose

Then inside ¨compose¨ folder create 2 folders at root level of the Vagrant-project. Execute the following:

- mkdir app
- mkdir proxy

Inside the ¨app¨ folder create a file called ¨Dockerfile¨ and put the following code inside of it:

https://github.com/marcossv9/devops-challenge/blob/master/compose/app/Dockerfile

Also write this HTML example at the same foler (name it ¨index.html¨):

https://github.com/marcossv9/devops-challenge/blob/master/compose/app/index.html

Now inside the ¨proxy¨ folder create a file called ¨Dockerfile¨ and put the following code inside of it:

https://github.com/marcossv9/devops-challenge/blob/master/compose/proxy/Dockerfile

Also create a file called ¨proxy.conf¨ that contains all the proxy config for NGINX. You can use this code:

https://github.com/marcossv9/devops-challenge/blob/master/compose/proxy/proxy.conf

**Create a Docker Compose file to create and execute the Containers defined in the Dockerfiles created before**

Inside the ¨compose¨ folder create a file called ¨docker-compose.yml¨ with this code inside:

https://github.com/marcossv9/devops-challenge/blob/master/compose/docker-compose.yml

**Configure Ansible-playbook to provision changes to the VM at startup**

Create a file in the same directory called ¨playbook.yml¨ y fill it with the code here:

https://github.com/marcossv9/devops-challenge/blob/master/playbook.yml

**Create the VM with all the described before**

You have to use move to ¨Vagrant-Project¨ folder and execute the following command:

- sudo vagrant up

**Test the website**

Test the website using a browser of preference going to this IP from your Host machine:

- http:127.0.0.1:8080