# Atividade Compass

## Criar máquina virtual
Obter imagem _Oracle Linux_ em:
https://yum.oracle.com/oracle-linux-isos.html

Obter instalador _VirtualBox_: 
https://www.virtualbox.org/wiki/Downloads

Em _Software Selection_ alterar a opção para _Minimal Install_
![Captura de tela 2022-07-05 132402](https://user-images.githubusercontent.com/108694840/177373712-fe9bc1fa-cc3d-408f-b2cb-5f4453a38e9b.png)

Em _Installation Destination_ alterar _Storage Configuration_ para a opção _Custon_


## Instalar e configurar GitHub
Instalar Git
```
$ sudo yum install git-all
```
Criar repositório de arquivos
```
$ mkdir repositorio-git
```
Acessar repositório
```
$ cd repositorio-git
```
Iniciar o Git dentro do repositório
```
$ git init
```
Vincular ao repositório remoto
```
$ git remote add origin github.com/Ryan-Amaro/Atividade-Compass.git
```


## Subir arquivos para o GitHub
Exibir status de arquivos do repositório local
```
$ git status
```
Adicionar arquivo ao commit
```
$ git add nome_do_arquivo
```
Salvar localmente usuário e senha do repositório Git
```
$ git config credential.helper store
$ git config --global credential.helper store
```
> Armazena localmente o usuário e a senha digitados, evitando a necesidade de digitar constantemente.

Descrição do commit
```
$ git commit -m "digite uma mensagem"
```
Enviar arquivo para o repositório Git
```
$ git push -u origin
```
> Na primeira vez em que este comando é executado, será pedido o usuário e o código do token.


## Configurar rede: 
Entrar como root
```
$ su
```
Obter endereço ip
```
# curl ifconfig.me 
```
Alterar configurações da placa de rede
```
# vi /etc/sysconfig/network-scripts/ifcfg-enp0s3 
```
```
BOOTPROTO=static 

IPADDR=000.000.000.000 

NETMASK=255.255.255.0 
```
> Alterar e inserir novos parâmetros

> Substituir os zeros pelo número do ip

Alterar hostname
```
# vi /etc/hostname 
```
```
oracle-linux.localdomain 
```
> Substituir nome padrão por "oracle-linux"
```
# vi /etc/sysconfig/network 
```
```
NETWORKING=yes 

HOSTNAME=oracle-linux 

GATEWAY=10.0.2.2     
```


## Configurar de SSH: 
Bloquear acesso root via ssh
```
# vi /etc/ssh/sshd_config 
```
Alterar parâmetro
```
PermitRootLogin no 
```
Reestartar serviço ssh
```
# systemctl restart sshd    
```


## Acessar remotamente via SSH
Abra o _Prompt de Comando_ e digite
```
ssh -p 2222 nome_do_usuario@127.0.0.1
```
> Preencher com nome de usuário do Linux


## Instalar e configurar Docker: 
```
$ sudo dnf install dnf-plugins-core
```
```
$ sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo 
```
```
$ sudo dnf install docker-ce docker-ce-cli containerd.io 
```
```
$ sudo systemctl start docker 
```
```
$ sudo systemctl enable docker 
```
Reiniciar sistema
```
$ shutdown -r now 
```
Mostrar serviço Docker ativo
```
$ systemctl status docker 
```
Executar imagem de teste
```
$ sudo docker run hello-world 
```
Definir usuário com privilégios no docker
```
$ sudo groupadd docker 
```
```
$ sudo usermod -aG docker nome_do_usuário 
```
```
$ newgrp docker 
```


## Instalar e configurar container ELK: 
Baixar imagem
```
$ docker pull sebp/elk 
```
Consultar imagens instaladas
```
$ docker images 
```
Executar container
```
$ docker run -d --restart unless-stopped -p 5601:5601 -p 9200:9200 -p 5044:5044 -it id_imagem
```
Exibir containers ativos
```
$ docker ps
```
Renomear container
```
$ docker rename id_container elk 
```
