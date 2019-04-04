VRMaster Files

Para instalar o VRMaster no Linux basta apenas montar a pasta do servidor e executar a partir da montagem.

Montando diretório do servidor

sudo mount //ip_do_servidor/vr /diretorio_da_montagem/ -o username=vr,password=pdv

Nesse caso sempre que a máquina reiniciar será necessário montar novamente. Basta executar o comando abaixo e sempre que o OS iniciar ele vai montar o diretório.

echo //ip_do_servidor/vr /diretorio_da_montagem cifs username=vr,password=pdv 0 0 >> /etc/fstab
