LINK PARA BAIXAR A IMAGEM DO DEBIAN 11

https://ufpabr-my.sharepoint.com/:f:/r/personal/andre_carvalho_silva_itec_ufpa_br/Documents/Descaracteriza%C3%A7%C3%A3o%20da%20TV%20Box/Cluster?csf=1&web=1&e=zl8N4x

Para configurar um IP fixo no Debian

sudo nano /etc/netplan/<tecla:tab>


# Instalação do PBS
Clonar o diretório do PBS:
sudo apt install git && git clone https://github.com/openpbs/openpbs.git

Pacotes pedidos no git hub:
sudo apt-get update && sudo apt-get upgrade && sudo apt-get install gcc make libtool libhwloc-dev libx11-dev libxt-dev libedit-dev libical-dev ncurses-dev perl postgresql-server-dev-all postgresql-contrib python3-dev tcl-dev tk-dev swig libexpat-dev libssl-dev libxext-dev libxft-dev autoconf automake g++ expat libedit2 postgresql python3 postgresql-contrib sendmail-bin sudo tcl tk libical3

Pacotes pedidos no PDF:
sudo apt update && sudo apt upgrade && sudo apt install gcc make libtool libhwloc-dev libx11-dev libxt-dev libedit-dev ncurses-dev perl postgresql-server-dev-all postgresql-contrib python-dev tcl-dev tk-dev swig libexpat-dev libssl-dev libxext-dev libxft-dev autoconf automake git expat libedit2 postgresql python postgresql-contrib sendmail-bin tcl tk libical3 libglew-dev mpich

# Compilando o PBS:
cd openpbs/ && cd m4 && sed -i 's/x86_64-linux-gnu/arm-linux-gnueabihf/g' *.m4 && cd ..

./autogen.sh && ./configure -prefix=/opt/pbs && make && sudo make install

# Pós compilação pbs:
sudo /opt/pbs/libexec/pbs_postinstall
sudo nano /etc/pbs.conf #Deve configurar os parâmetros
sudo chmod 4755 /opt/pbs/sbin/pbs_iff /opt/pbs/sbin/pbs_rcp
sudo /etc/init.d/pbs start

# Configurando server, filas e nós:
sudo /opt/pbs/bin/qmgr
create queue <nome da fila> queue_type=e,started=t,enabled=t
set server default_queue=<nome da fila>
set server job_history_enable=true
set server flatuid=true
create node <nome do nó>
exit

pbsnodes -a
