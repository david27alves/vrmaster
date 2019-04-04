## Install MATE Desktop CentOS 7

```sh
$ sudo yum install epel-release -y
$ sudo yum groupinstall "Development Tools" -y
$ sudo yum groupinstall "X Window system" -y
$ sudo yum groups install "MATE Desktop" -y
$ systemctl isolate graphical.target
$ systemctl set-default graphical.target 
```

## Install Firebird

```sh
$ tar -xvf FirebirdCS-2.5.3.26780-0.amd64.tar.gz 
$ cd FirebirdCS-2.5.2.26540-0.i686
$ sudo ./install
$ sudo /etc/init.d/firebird start
$ chkconfig firebird on
```

## Install Anydesk

```sh
$ sudo rpm -ivh mesa-libGLU-9.0.0-4.el7.x86_64.rpm anydesk-4.0.1-1.el7.x86_64.rpm
```



## Instalação do Postgres no CentOS

Iso CentOS 7 Minimal 64bits
	
http://mirror.ufscar.br/centos/7/isos/x86_64/CentOS-7-x86_64-Minimal-1708.iso


Após a instalação e reinicio do CentOS 7

```sh
sudo -i
Usuário e Senha
```

Definição do IP

```sh
vim /etc/sysconfig/network-scripts/ifcfg-eth0 (Nome da Placa de Rede) 

DEVICE= Nome da Placa de Rede
TYPE= Ethernet
IPADDR= IP
NETMASK= Mascara
GATEWAY= GW
```

```sh
service network restart
```

Configurando SSH

```sh
vi /etc/ssh/sshd_config
```

```sh
	PermitRootLogin = no
```
		
Desabilitando o Firewall

```sh
systemctl disable firewalld
systemctl stop firewalld
```
   		
Instalação do Postgresql

```sh

yum localinstall http://yum.postgresql.org/9.5/redhat/rhel-6-x86_64/pgdg-centos95-9.5-3.noarch.rpm
yum list postgresql
yum install postgresql95-server
yum install postgres*95*contrib
```

Criar o banco de dados

```sh
/usr/pgsql-9.5/bin/postgresql95-setup initdb
```

Alteração pg_hba e Postgresql

```sh
vi /var/lib/pgsql/9.5/data/pg_hba.conf	
```

Altera o necessário e descomenta a linha

```sh
# IPv4 local connections: Trust
host    all             all             0.0.0.0/0            trust
```

```sh
	vi /var/lib/pgsql/9.5/data/postgresql.conf
```

Altera o necessário e descomenta a linha

```sh
Localhost = '*'
datestyle = 'iso, mdy'
standard_conforming_strings = off
enable_seqscan = off
	
tcp_keepalives_idle = 10
tcp_keepalives_interval = 10
tcp_keepalives_count = 10
	
logging_colletor = off
log_directory = 'pg_log'
log_truncate_on_rotation = on
log_rotation_age = 2d
log_rotation_size = 20MB
```		

Inicializar com o Linux

```sh
chkconfig postgresql-9.5 on
service postgresql-9.5 restart
```

```sh
vi /etc/selinux/config
```

```sh
selinux=disabled
```
```sh
init 6
```sh

Backup Linux

```sh
vi /etc/crontab 			Define os horarios e usuário do backup
```

```sh
cp bk_vr-yum /usr/bin/		Copiar o bk_vr-yum para a pasta Bin    	- Alterar a versão do postgres no arquivo e acrescentar -p + porta quando não for a padrão
```

Criar a pasta VR na raiz (/)

```sh
mkdir /vr
```

```sh
chmod -R 2777 /vr
```

|Samba|

```sh
yum install samba
```

```sh
vi /etc/samba/smb.conf
```
	
[global]
	
Adicionar abaixo do security

```sh	
map to guest = bad user
```

No final do arquivo adicionar as linhas de comentários

```sh
[vr]

coment = vr
path = /vr
public = yes
writable = yes
create mask = 2777
directory mask = 2777
```

```sh
firewall-cmd --permanent --zone=public --add-service=samba
```

```sh
firewall-cmd --reload
```

Salva o arquivo
	
					
Serviço Samba

```sh
systemctl enable smb.service
```

```sh
systemctl enable nmb.service
```

```sh
systemctl restart smb.service
```

```sh
systemctl restart nmb.service
```

```sh
chcon -t samba_share_t vr/   (fazer esse comando dentro de /)
```
