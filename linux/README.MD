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
