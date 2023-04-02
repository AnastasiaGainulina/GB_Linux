# Урок 4. Подключение сторонних репозиториев, ручная установка пакетов
#### Задание:
###### 1. Подключить дополнительный репозиторий на выбор: Docker, Nginx, Oracle MySQL. Установить любой пакет из этого репозитория.
###### 3. Установить и удалить snap-пакет.

gb@gb-linux:~$
gb@gb-linux:~$ lsb_release -a

gb@gb-linux:~$ echo "deb http://nginx.org/packages/ubuntu focal nginx" > nginx.list
gb@gb-linux:~$ curl -fsSL https://nginx.org/keys/nginx_signing.key | sudo apt-key add -

gb@gb-linux:~$ sudo snap install curl # version 8.0.1

gb@gb-linux:~$ curl -fsSL https://nginx.org/keys/nginx_signing.key | sudo apt-key add -

gb@gb-linux:~$ sudo apt update

gb@gb-linux:~$ sudo apt install nginx -y


###### 2. Установить и удалить deb-пакет с помощью dpkg.
root@gb-linux:~# wget https://download.virtualbox.org/virtualbox/7.0.6/virtualbox-7.0_7.0.6-155176~Ubuntu~jammy_amd64.deb


root@gb-linux:~# dpkg -i virtualbox-7.0_7.0.6-155176~Ubuntu~jammy_amd64.deb

root@gb-linux:~# apt -f install

Хотите продолжить? [Д/н] y

root@gb-linux:~# cd /etc/apt
root@gb-linux:/etc/apt# ll

root@gb-linux:/etc/apt# cd sources.list.d/
root@gb-linux:/etc/apt/sources.list.d# ll

root@gb-linux:/etc/apt/sources.list.d# nano
root@gb-linux:/etc/apt/sources.list.d# nano vb.list
root@gb-linux:/etc/apt/sources.list.d# root@gb-linux:/etc/apt/sources.list.d# nano vb.list
root@gb-linux:/etc/apt/sources.list.d# apt update
root@gb-linux:/etc/apt/sources.list.d# wget -O- https://www.virtualbox.org/download/oracle_vbox_2016.asc | sudo gpg --dearmor --yes --output /usr/share/keyrings/oracle-virtualbox-2016.gpg

root@gb-linux:/etc/apt/sources.list.d# apt update

root@gb-linux:/home/gb# dpkg -r virtualbox-7.0



####### 4. Добавить задачу для выполнения каждые 3 минуты (создание директории, запись в файл).

gb@gb-linux:~$ crontab -e
0/3 * * * * /usr/bin/mkdir /qwerty && sleep 5m && /usr/bin/touch /qwerty/file1
