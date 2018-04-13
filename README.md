# Devops-Challenge - VERSIÓN BETA

Un despliegue rápido de un sitio web usando Vagrant + VirtualBox + Ansible + DockerCompose

## Requisitos de versión de herramientas que usaremos:

1. Version VirtualBox: 5.2-5.2.8_121009
2. Version Vagrant: 2.0.3 

## Para poner todo en marcha de la forma fácil y rápida:

1. Instalar VirtualBox & Vagrant (si no están instalado ya)
2. Clonar el repo devops-challenge con ```# git clone https://github.com/marcossv9/devops-challenge``` y colóquelo en el directorio desde el que desea iniciar la VM.
3. Navegar al directorio de repos local e inicie la VM con Vagrant usando el comando ```# sudo vagrant up```
4. A disfrutar!

## Si desea hacer todo manualmente, siga estos pasos:

** Instalar VirtualBox **

Vaya a https://www.virtualbox.org/wiki/Linux_Downloads y descargue e instale la versión de VBOX para su sistema operativo.

En mi caso, descargo el archivo -> https://download.virtualbox.org/virtualbox/5.2.8/VirtualBox-5.2-5.2.8_121009_openSUSE132-1.x86_64.rpm

Yo lo instalé con el comando ```# sudo zypper in VirtualBox-5.2-5.2.8_121009_openSUSE132-1.x86_64.rpm ```

** Instalar Vagrant **

Vaya a https://www.vagrantup.com/downloads.html y siga los pasos para instalar Vagrant en su sistema operativo preferido.

En este caso, uso OpenSuseLEAP para lo que el comando que usé fue ```# sudo zypper en vagrant_2.0.3_x86_64rpm```

** Crear un directorio donde vas a trabajar con Vagrant **

Los comandos en orden son: ```# mkdir Vagrant-Project``` y luego moverse al directorio con el comando ```# cd Vagrant-Project```

** Iniciar Vagrant para generar un Vagrantfile en el directorio actual **

Utilizar el comando ```# init vagrant```

** Editar el Vagrantfile para definir una VM con Docker Engine y Docker-compose. A continuación se ejecutará un Ansible-playbook local para iniciar dos Contenedores Docker dentro de la VM utilizando Docker Compose **

Aquí está el archivo Vagrant con comentarios para entender cada línea del archivo:

https://github.com/marcossv9/devops-challenge/blob/master/Vagrantfile

** Crear dos archivos Docker que Docker Compose ejecutará y ejecutará un sitio web y un servidor proxy **

Crear una carpeta para Docker Compose donde va a alojar dos Dockerfile, uno para el servidor web y otro para el servidor proxy. Usar el comando ```# mkdir compose```

Luego, dentro de la carpeta ¨compose¨ crear 2 carpetas en el nivel raíz del directorio ¨Vagrant-Project¨. Ejecutar lo siguientes comandos en orden: ```# mkdir app``` y ```# mkdir proxy```

Dentro de la carpeta "app" crear un archivo llamado "Dockerfile" y escibir el siguiente código dentro de él:

https://github.com/marcossv9/devops-challenge/blob/master/compose/app/Dockerfile

También descargue y copie en el directorio ¨app¨, el contenido del directorio ¨site¨, el cual contendrá nuestra página web de pruebas. EL link de descarga es el siguiente:

https://github.com/marcossv9/devops-challenge/tree/master/compose/app/site

Ahora dentro de la carpeta "proxy" crear un archivo llamado "Dockerfile" y escribir el siguiente código dentro de él:

https://github.com/marcossv9/devops-challenge/blob/master/compose/proxy/Dockerfile

Crear también un archivo llamado "proxy.conf" dentro de la carpeta ¨proxy¨, que contenga toda la configuración del proxy para NGINX. Se debe usar este código:

https://github.com/marcossv9/devops-challenge/blob/master/compose/proxy/proxy.conf

** Crear un archivo Docker Compose para crear y ejecutar los Contenedores definidos en los Dockerfile creados antes **

Dentro de la carpeta ¨compose¨ crear un archivo llamado ¨docker-compose.yml¨ con este código adentro:

https://github.com/marcossv9/devops-challenge/blob/master/compose/docker-compose.yml

** Configurar Ansible-playbook para aprovisionar cambios en la máquina virtual al inicio **

Crear un archivo en el directorio raíz del projecto (Vagrant-Project) y llamarlo ¨playbook.yml¨ y escribir el código que aquí se menciona:

https://github.com/marcossv9/devops-challenge/blob/master/playbook.yml

** Crear la VM con todo lo descrito antes **

Tienes que moverte a la carpeta ¨Vagrant-Project¨ y ejecutar el siguiente comando ```# sudo vagrant up```

** Probar el sitio web **

Pruebe el sitio web usando un navegador de preferencia y vaya a la siguiente URL desde su máquina Host:

- http://127.0.0.1:8080

## Recursos utilizados

Template de website descargado de http://www.free-css.com/free-css-templates/page226/app-starter