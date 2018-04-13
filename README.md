# Devops-Challenge - VERSIÓN BETA

Un despliegue rápido de un sitio web usando Vagrant + VirtualBox + Ansible + DockerCompose

## Requisitos de versión de herramientas que usaremos:

1. Version Virtual Box: 5.2-5.2.8_121009
2. Version Vagrant: 2.0.3 

## Para poner todo en marcha:

1. Instalar Virtual Platform & Vagrant (si no está instalado ya)
2. Clone devops-challenge git repo # git clone https://github.com/marcossv9/devops-challenge y colóquelo en el directorio desde el que desea iniciar el vagabundo.
3. Navegue al directorio de repos local y comience vagabundo ```# sudo vagrant up```
4. Disfruta

## Si desea hacer todo manualmente, siga estos pasos:

** Instalar VirtualBox **

Vaya a https://www.virtualbox.org/wiki/Linux_Downloads y descargue e instale la versión de VBOX para su sistema operativo.

En mi caso, descargo el archivo -> https://download.virtualbox.org/virtualbox/5.2.8/VirtualBox-5.2-5.2.8_121009_openSUSE132-1.x86_64.rpm

Y lo instalé con el comando:

- sudo zypper en VirtualBox-5.2-5.2.8_121009_openSUSE132-1.x86_64.rpm

** Instalar Vagrant **

Vaya a https://www.vagrantup.com/downloads.html y siga los pasos para instalar Vagrant en su sistema operativo preferido.

En este caso, uso OpenSuseLEAP para que el comando sea:

- sudo zypper en vagrant_2.0.3_x86_64rpm

** Crea un directorio donde vas a trabajar con Vagrant

- mkdir Vagrant-Project
- Proyecto cd Vagrant

** Init Vagrant para generar un Vagrantfile en el directorio actual **

- init vagabundo

** Edite el Vagrantfile para definir una VM con Docker Engine y Docker-compose. A continuación, ejecutará un libro de respuestas de Ansible local para iniciar dos Contenedores Docker dentro de la VM utilizando Docker Compose **

Aquí está el archivo Vagrant con comentarios para entender cada línea del archivo:

https://github.com/marcossv9/devops-challenge/blob/master/Vagrantfile

** Crea dos archivos Docker que Docker Compose ejecutará y ejecutará un sitio web y un servidor proxy **

Cree una carpeta de compilación de portlet donde va a alojar dos archivos Doker para el servidor web y el servidor proxy. Usa el comando:

- mkdir componer

Luego, dentro de la carpeta ¨compose¨ crea 2 carpetas en el nivel raíz del proyecto Vagrant. Ejecuta lo siguiente:

- Aplicación mkdir
- mkdir proxy

Dentro de la carpeta "App" crea un archivo llamado "Dockerfile" y escibir el siguiente código dentro de él:

https://github.com/marcossv9/devops-challenge/blob/master/compose/app/Dockerfile

También descargue y copie el contenido del directorio ¨site¨, el cual contendrá nuestra página web de pruebas. EL link de descarga es el siguiente:

https://github.com/marcossv9/devops-challenge/tree/master/compose/app/site

Ahora dentro de la carpeta "proxy" crea un archivo llamado "Dockerfile" y escribir el siguiente código dentro de él:

https://github.com/marcossv9/devops-challenge/blob/master/compose/proxy/Dockerfile

Cree también un archivo llamado "proxy.conf" que contenga toda la configuración del proxy para NGINX. Puedes usar este código:

https://github.com/marcossv9/devops-challenge/blob/master/compose/proxy/proxy.conf

** Cree un archivo Docker Compose para crear y ejecutar los Contenedores definidos en los archivos Docker creados antes **

Dentro de la carpeta ¨compose¨ crea un archivo llamado ¨docker-compose.yml¨ con este código adentro:

https://github.com/marcossv9/devops-challenge/blob/master/compose/docker-compose.yml

** Configure Ansible-playbook para aprovisionar cambios en la máquina virtual al inicio **

Crea un archivo en el mismo directorio llamado ¨playbook.yml¨ y llénalo con el código aquí:

https://github.com/marcossv9/devops-challenge/blob/master/playbook.yml

** Crea la VM con todo lo descrito antes **

Tienes que moverte a la carpeta ¨Vagrant-Project¨ y ejecutar el siguiente comando:

- sudo vagrant up

** Pruebe el sitio web **

Pruebe el sitio web usando un navegador de preferencia que vaya a esta IP desde su máquina Host:

- http: 127.0.0.1: 8080