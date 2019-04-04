Para instalar o VRMaster no Linux basta apenas montar a pasta do servidor e executar a partir da montagem.

Montando diretório do servidor

```sh
sudo mount //ip_do_servidor/vr /diretorio_da_montagem/ -o username=vr,password=pdv
```

Nesse caso sempre que a máquina reiniciar será necessário montar novamente. Basta executar o comando abaixo e sempre que o OS iniciar ele vai montar o diretório.

```sh
echo //ip_do_servidor/vr /diretorio_da_montagem cifs username=vr,password=pdv 0 0 >> /etc/fstab
```

Próximo passo é criar o atalho na área de trabalho. Crie um arquivo com o nome VRMaster.desktop na Área de Trabalho e adicione o seguinte conteúdo.

```sh
#!/usr/bin/env xdg-open
[Desktop Entry]
Name=VRMaster
Exec=java -jar /caminho/do/VRMaster.jar
Icon=/caminho/do/icone/VRMaster.ico
Type=Application
Categories=VR
```
