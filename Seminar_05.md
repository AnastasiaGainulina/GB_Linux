# Урок 5. Настройка сети в Linux. Работа с IPtables
### Задание:
###### 1 Настроить статическую конфигурацию (без DHCP) в Ubuntu через ip и netplan. Настроить IP, маршрут по умолчанию и DNS-сервера (1.1.1.1 и 8.8.8.8). Проверить работоспособность сети.
network:
    version: 2
    renderer: network
    ethernets:
        enp0s3:
            dhcp4: no
            addresses: [192.168.0.8/24]
            routes:
                - to: default
                via: 192.168.0.254
            nameservers:
                addresses:
                    -8.8.8.8
                    -1.1.1.1

sudo ip addr 192.168.0.9/255.255.255.0 broadcast 192.168.0.255
dev enp0s3
ping ya.ru


###### 2 Настроить правила iptables для доступности сервисов на TCP-портах 22, 80 и 443. Также сервер должен иметь возможность устанавливать подключения к серверу обновлений. Остальные подключения запретить.

iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -p TCP --dport 22 -j ACCEPT
iptables -A INPUT -p TCP --dport 80 -j ACCEPT
iptables -A INPUT -p TCP --dport 443 -j ACCEPT
iptables -A INPUT -m state --state ESTABLISHED, RELATED -j ACCEPT
iptables -P INPUT DROP

###### 3 Запретить любой входящий трафик с IP 3.4.5.6.
iptables -I INPUT -s 3.4.5.6 -j DROP


###### 4* Запросы на порт 8090 перенаправлять на порт 80 (на этом же сервере).
iptables -t nat -I PREROUTING -p tcp --dport 8090 -j REDIRECT

###### 5* Разрешить подключение по SSH только из сети 192.168.0.0/24.
iptables -I INPUT -p TCP --dport 22 -j DROP
iptables -I INPUT -p TCP --dport 22 -s 192.168.0.0/24 -j ACCEPT
