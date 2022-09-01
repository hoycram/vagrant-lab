# vagrant-lab
Neste artigo vamos aprender a criar um Serviod Web usando como base o Vagrant e o Virtual Box.

1- É necessário baixar o Vagrant, Virtualbox, Git e Vscode nos links abaixo:
A) Vagrant (https://www.vagrantup.com/downloads);
B) Virtual Box (https://www.virtualbox.org/wiki/Downloads);
C) Vscode (https://code.visualstudio.com/download);
D) Git (https://git-scm.com/downloads)

Depois que realizar as intalações dos softwares acima, daremos início aos passos abaixo:

A - Criar uma pasta chamada vagrant-lab;
B - Dentro da pasta abrir o Git Bash;
C - Executar o comando Vagrant init.

2- Após o comando vagrant init, dentro da pasta será criado o arquivo vagranfile, será 
necessário abrir o mesmo com Vscode. 

Com o Vscode aberto vamos digitar os seguintes códigos:

Vagrant.configure("2') do |config|
config.vm.box = "centos/7"
config.vm.network "forwarded_port", guest:80, host:8080, host_ip: "127.0.0.1"
config.vm.provision "shell", path: "provision.sh"
config.vm.host_name = "Servidor Web"
end

Explicando os códigos:

config.vm.box = "centos/7" = Sistema operacional que for escolher;
config.vm.network "forwarded_port", guest:80, = porta do seu computador ou host por padrão, sempre é aconselhado a usar portas acima de 1024;
host: 8080 = trocado para esta porta ao invés de fazer uso da porta 80;
host_ip: "127.0.0.1" = endereço do servidor local, é caminho que deverá digitar no navegador, podendo ser substituido por localhost:8080;
config.vm.provision "shell", = Tipo de arquivo que será executado em shell;
path: "provision.sh" = Caminho do arquivo que tem a instalação dos serviços ou softwares. 

3- Criando o arquivo provision.sh, dentro do arquivos vamos digitar os comandos abaixo:

#!/usr/bin/env bash
echo "Instalando o Servidor Web"
yum install -y httpd >/dev/null 2>&1
cp -r /vagrant/html/* /var/wwww/html/
service httpd start

Explicando o código:

#!/usr/bin/env bash = Informa que será em um terminal bash ou comandos linux;

yum install -y = Instalar os packages yum que auxilia a instalar os demais plugins;

httpd >/dev/null 2>&1 = Instalar o apache;

cp -r /vagrant/html/* Copiar tudo desta pasta, localizada no seu computador local, para dentro do servido neste caminho =>/var/www/html/;

service httpd start, toda vez que iniciar o computador ele vai startar o serviço http.

Obs: Na pasta em que se encontra os arquivos vagranfile e provision.sh, você deverá criar uma pasta chamada html e dentro desta pasta, colocar todos 
os arquivos CSS, JavaScript e HTML. 

Espero ter contribuído com o seu conhecimento. 
Agradecimentos ao Professor: Glaucio Guerra
Perfil dele na Udemy: https://www.udemy.com/user/glaucio-guerra/
