hostname VST26-SF30024-1
enable password level 15 encrypted ea75da09d8596d4e2314861686fd33903c59020e
passwords aging 0 
username ctadmin password encrypted ea75da09d8596d4e2314861686fd33903c59020e privilege 15 
ip ssh server
snmp-server server
snmp-server location "Armavir, Efremova, 162 [44.99686,41.10866]"
snmp-server contact noc@city-telekom.ru
snmp-server community public ro 10.5.0.11 view Default 
snmp-server community t0LmsCrRxU ro 10.5.0.9 view Default 
snmp-server host 10.5.0.11 traps version 2c public 
clock timezone MSK +3
sntp anycast client enable both 
sntp broadcast client enable both 
clock source sntp
sntp unicast client enable
sntp unicast client poll
sntp server 10.5.0.4 poll 
sntp server 10.5.0.29 poll 
ip telnet server
!
interface vlan 445
 name CUST 
 ip dhcp relay enable 
!
interface vlan 446
 name MGNT 
 ip address 10.5.194.212 255.255.255.224 
!

!
interface fastethernet1
 loopback-detection enable 
 description PPPoE-441
 bridge multicast unregistered filtering 
 storm-control broadcast enable 
 storm-control broadcast level kbps 70 
 storm-control include-multicast 
 spanning-tree disable 
 spanning-tree guard root 
 switchport mode access 
 switchport access vlan 481 
 no cdp enable 
!
interface fastethernet2
 loopback-detection enable 
 description PPPoE-19174
 bridge multicast unregistered filtering 
 storm-control broadcast enable 
 storm-control broadcast level kbps 70 
 storm-control include-multicast 
 spanning-tree disable 
 spanning-tree guard root 
 switchport mode access 
 switchport access vlan 481 
 no cdp enable 
!
interface fastethernet3
 loopback-detection enable 
 bridge multicast unregistered filtering 
 storm-control broadcast enable 
 storm-control broadcast level kbps 70 
 storm-control include-multicast 
 spanning-tree disable 
 spanning-tree guard root 
 switchport mode access 
 switchport access vlan 481 
 no cdp enable 
!
interface fastethernet4
 loopback-detection enable 
 description PPPoE-18251
 bridge multicast unregistered filtering 
 storm-control broadcast enable 
 storm-control broadcast level kbps 70 
 storm-control include-multicast 
 spanning-tree disable 
 spanning-tree guard root 
 switchport mode access 
 switchport access vlan 481 
 no cdp enable 
!
interface fastethernet5
 loopback-detection enable 
 description 56875-kv36
 bridge multicast unregistered filtering 
 storm-control broadcast enable 
 storm-control broadcast level kbps 70 
 storm-control include-multicast 
 spanning-tree disable 
 spanning-tree guard root 
 switchport mode access 
 switchport access vlan 481 
 no cdp enable 
!
interface fastethernet6
 loopback-detection enable 
 bridge multicast unregistered filtering 
 storm-control broadcast enable 
 storm-control broadcast level kbps 70 
 storm-control include-multicast 
 spanning-tree disable 
 spanning-tree guard root 
 switchport mode access 
 switchport access vlan 481 
 no cdp enable 
!
interface fastethernet7
 loopback-detection enable 
 description PPPoE-842
 bridge multicast unregistered filtering 
 storm-control broadcast enable 
 storm-control broadcast level kbps 70 
 storm-control include-multicast 
 spanning-tree disable 
 spanning-tree guard root 
 switchport mode access 
 switchport access vlan 481 
 no cdp enable 
!
interface fastethernet8
 loopback-detection enable 
 bridge multicast unregistered filtering 
 storm-control broadcast enable 
 storm-control broadcast level kbps 70 
 storm-control include-multicast 
 spanning-tree disable 
 spanning-tree guard root 
 switchport mode access 
 switchport access vlan 481 
 no cdp enable 
!
interface fastethernet9
 loopback-detection enable 
 bridge multicast unregistered filtering 
 storm-control broadcast enable 
 storm-control broadcast level kbps 70 
 storm-control include-multicast 
 spanning-tree disable 
 spanning-tree guard root 
 switchport mode access 
 switchport access vlan 481 
 no cdp enable 
!
interface fastethernet10
 loopback-detection enable 
 bridge multicast unregistered filtering 
 storm-control broadcast enable 
 storm-control broadcast level kbps 70 
 storm-control include-multicast 
 spanning-tree disable 
 spanning-tree guard root 
 switchport mode access 
 switchport access vlan 481 
 no cdp enable 
<details>
  <summary>RTR</summary>



```
config
hostname name
do commit
do confirm
```


```
sh ip int
sh int stat
```

```
interface te1/0/2
ip address 11.11.11.2/30
description ISP
exit
```

```
domain name company.prof
domain name-server 11.11.11.1
```

```
ip route 0.0.0.0/0 11.11.11.1
```

```
interface te1/0/3.100
ip firewall disable
description vlan100
ip address 10.0.10.1/27
exit
```

```
interface te1/0/3.200
ip firewall disable
description vlan200
ip address 10.0.10.33/27
exit
```

```
interface te1/0/3.300
ip firewall disable
description vlan300
ip address 10.0.10.65/27
exit
```

```
do commit
do confirm
```

Все остальное

```
hostnamectl set-hostname <VM_NAME>.company.prof;exec bash
```

```
sed -i 's/DISABLED=yes/DISABLED=no/g' /etc/net/ifaces/ens18/options
sed -i 's/NM_CONTROLLED=yes/NM_CONTROLLED=no/g' /etc/net/ifaces/ens18/options
echo 10.0.20.2/24 > /etc/net/ifaces/ens18/ipv4address
echo default via 10.0.20.1 > /etc/net/ifaces/ens18/ipv4route
systemctl restart network
ping -c 4 8.8.8.8
```

```
adduser sshuser
passwd sshuser
P@ssw0rd
P@ssw0rd
echo "sshuser ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
usermod -aG wheel sshuser
sudo -i
```


```
mkdir /home/sshuser
```
```
chown sshuser:sshuser /home/sshuser
```
```
cd /home/sshuser
```
```
mkdir -p .ssh/
```
```
chmod 700 .ssh
```
```
touch .ssh/authorized_keys
```
```
chmod 600 .ssh/authorized_keys
```
```
chown sshuser:sshuser .ssh/authorized_keys
```

```
ssh-keygen -t rsa -b 2048 -f srv_ssh_key
```
```
mkdir .ssh
```
```
mv srv_ssh_key* .ssh/
```
```
Host srv-hq
        HostName 10.0.10.2
        User sshuser
        IdentityFile .ssh/srv_ssh_key
        Port 2023
Host srv-br
        HostName 10.0.20.2
        User sshuser
        IdentityFile .ssh/srv_ssh_key
        Port 2023
```
```
chmod 600 .ssh/config
```

```
ssh-copy-id -i .ssh/srv_ssh_key.pub sshuser@10.0.10.2
```
```
ssh-copy-id -i .ssh/srv_ssh_key.pub sshuser@10.0.20.2
```
`/etc/ssh/sshd_config`:
```
AllowUsers sshuser
PermitRootLogin no
PubkeyAuthentication yes
PasswordAuthentication no
AuthorizedKeysFile .ssh/authorized_keys
Port 2023
```
```
systemctl restart sshd
```

</details>

<details>
  <summary>nwxt</summary>
## 7.	Настройка DNS для SRV-HQ и SRV-BR

i.	Реализуйте основной DNS сервер компании на SRV-HQ  
&ensp; a.	Для всех устройств обоих офисов необходимо создать записи A и PTR.  
&ensp; b.	Для всех сервисов предприятия необходимо создать записи CNAME.  
&ensp; c.	Создайте запись test таким образом, чтобы при разрешении имени из левого офиса имя разрешалось в адрес SRV-HQ, а из правого – в адрес SRV-BR.  
&ensp; d.	Сконфигурируйте SRV-BR, как резервный DNS сервер. Загрузка записей с SRV-HQ должна быть разрешена только для SRV-BR.  
&ensp; e.	Клиенты предприятия должны быть настроены на использование внутренних DNS серверов  

<details>
  <summary>ТЫКНИ</summary>

### SRV-HQ

Установка bind и bind-utils:
```
apt-get update && apt-get install -y bind bind-utils
```
Конфиг:
```
nano /etc/bind/options.conf
```
```
listen-on { any; };
allow-query { any; };
allow-transfer { 10.0.20.2; }; 
```

![изображение](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/12ad33f9-2df1-47e7-ad7a-1788b2276c88)

Включаем resolv:
```
nano /etc/net/ifaces/ens18/resolv.conf
```
```
systemctl restart network
```
Автозагрузка bind:
```
systemctl enable --now bind
```
Создаем прямую и обратные зоны:
```
nano /etc/bind/local.conf
```

![изображение](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/74bbb72d-1577-413d-969c-bff4497d0b9c)

Копируем дефолты:
```
cp /etc/bind/zone/{localhost,company.db}
```
```
cp /etc/bind/zone/127.in-addr.arpa /etc/bind/zone/10.0.10.in-addr.arpa.db
```
```
cp /etc/bind/zone/127.in-addr.arpa /etc/bind/zone/20.0.10.in-addr.arpa.db
```
Назначаем права:
```
chown root:named /etc/bind/zone/company.db
```
```
chown root:named /etc/bind/zone/10.0.10.in-addr.arpa.db
```
```
chown root:named /etc/bind/zone/20.0.10.in-addr.arpa.db
```
Настраиваем зону прямого просмотра `/etc/bind/zone/company.prof`:

![изображение](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/9d3bddf9-e8db-4cfc-8971-b3a6ff0f38ac)

Настраиваем зону обратного просмотра `/etc/bind/zone/10.0.10.in-addr.arpa.db`:

![изображение](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/3fee1532-458b-4e10-967f-b858a4a43b63)

Настраиваем зону обратного просмотра `/etc/bind/zone/20.0.10.in-addr.arpa.db`:

![изображение](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/c9f18689-b324-4125-836d-91bdb23b1075)

Проверка зон:
```
named-checkconf -z
```
![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/d2de05e9-3830-4846-86a1-2974bb64dbf5)

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/e1b6fb80-63df-4cf5-8dd6-2f3d46a1dc3b)

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/21d53c0b-27d9-4af9-bbe3-b64035b0ffad)

### SRV-BR

Конфиг
```
vim /etc/bind/options.conf
```

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/e90d49ce-6735-4fdb-b44a-0b1c62b8305a)

Добавляем зоны

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/ea22291d-0b41-4044-a271-1fbb32f26185)

Резолв `/etc/net/ifaces/ens18/resolv.conf`:
```
search company.prof
nameserver 10.0.10.2
nameserver 10.0.20.2
```
Перезапуск адаптера:
```
systemctl restart network
```
Автозагрузка:
```
systemctl enable --now bind
```
SLAVE:
```
control bind-slave enabled
```

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/dc174c7e-e960-42c6-8b9d-7522df00989a)

Разрешение имени хоста test

### SRV-HQ

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/a73800a1-b7cf-48e3-8160-49b3b14a0060)

Копируем дефолт для зоны:
```
cp /etc/bind/zone/{localdomain,test.company.db}
```

Задаём права, владельца:
```
chown root:named /etc/bind/zone/test.company.db
```
Настраиваем зону:
```
vim /etc/bind/zone/test.company.db
```

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/ae1dcd6e-d5b9-4980-8105-d14b74905083)

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/c8735610-56d5-419b-bdc8-3efc48a969b0)

Перезапускаем:
```
systemctl restart bind
```

### SRV-BR
Добавляем зону `/etc/bind/local.conf`:

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/2d279b81-8bfd-453b-8efa-dc3d87476c40)

Задаём права, владельца:
```
chown root:named /etc/bind/zone/test.company.db
```

Редактируем зону `/etc/bind/zone/test.company.db`:

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/1aa398ac-dd3a-4887-b975-14ff7a3bf633)

Перезапускаем:
```
systemctl restart bind
```

</details>

## 8.	Настройка узла управления Ansible

a)	Настройте узел управления на базе SRV-BR  
&ensp; a.	Установите Ansible.  
b)	Сконфигурируйте инвентарь по пути /etc/ansible/inventory. Инвентарь должен содержать три группы устройств:  
&ensp; a.	Networking  
&ensp; b.	Servers  
&ensp; c.	Clients  
c)	Напишите плейбук в /etc/ansible/gathering.yml для сбора информации об IP адресах и именах всех устройств (и клиенты, и серверы, и роутеры). Отчет должен быть сохранен в /etc/ansible/output.yaml, в формате ПОЛНОЕ_ДОМЕННОЕ_ИМЯ – АДРЕС  

<details>
  <summary>ТЫКНИ</summary>

Установка:
```
apt-get install -y ansible sshpass
```
```
vim /etc/ansible/inventory.yml
```

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/4c242402-3a03-43e2-8787-e66ba00b0e56)

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/6f656c35-a863-476d-a3a4-52dee8117017)

```
cd /etc/ansible
```
```
mkdir group_vars
```
```
vim group_vars/Networking.yml
```

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/4697fc7a-4b22-4c6f-a9ec-6a47b66b1809)

```
vim group_vars/Servers.yml
```

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/d07a5898-8852-4890-8eaa-4c8269d68e1d)

```
vim group_vars/Clients.yml
```

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/8100d601-0482-4e7a-aecd-0671f2a39d90)

```
vim group_vars/all.yml
```

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/a3c7e3de-d1fb-4a08-bc55-cc0765404a36)

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/f2ccec52-702a-4ba5-8c61-ba3dd9c5d147)

</details>

## 9.	Между маршрутизаторами RTR-HQ и RTR-BR сконфигурируйте защищенное соединение

a)	Все параметры на усмотрение участника.  
b)	Используйте парольную аутентификацию.  
c)	Обеспечьте динамическую маршрутизацию: ресурсы одного офиса должны быть доступны из другого офиса.  
d)	Для обеспечения динамической маршрутизации используйте протокол OSPF.  

https://sysahelper.gitbook.io/sysahelper/main/telecom/main/vesr_greoveripsec

<details>
  <summary>ТЫКНИ</summary>

```
tunnel gre 1
  ttl 16
  ip firewall disable
  local address 11.11.11.11
  remote address 22.22.22.22
  ip address 172.16.1.1/30
  enable
exit
```
```
security zone-pair public self
  rule 1
    description "ICMP"
    action permit
    match protocol icmp
    enable
  exit
  rule 2
    description "GRE"
    action permit
    match protocol gre
    enable
  exit
exit
```

```
security ike proposal ike_prop1
  authentication algorithm md5
  encryption algorithm aes128
  dh-group 2
exit
```

```
security ike policy ike_pol1
  pre-shared-key ascii-text P@ssw0rd
  proposal ike_prop1
exit
```

```
security ike gateway ike_gw1
  ike-policy ike_pol1
  local address 11.11.11.11
  local network 11.11.11.11/32 protocol gre 
  remote address 22.22.22.22
  remote network 22.22.22.22/32 protocol gre 
  mode policy-based
exit
```

```
security ike gateway ike_gw1
  ike-policy ike_pol1
  local address 22.22.22.22
  local network 22.22.22.22/32 protocol gre 
  remote address 11.11.11.11
  remote network 11.11.11.11/32 protocol gre 
  mode policy-based
exit
```

```
security ipsec proposal ipsec_prop1
  authentication algorithm md5
  encryption algorithm aes128
  pfs dh-group 2
exit
```

```
security ipsec policy ipsec_pol1
  proposal ipsec_prop1
exit
```
```
security ipsec vpn ipsec1
  ike establish-tunnel route
  ike gateway ike_gw1
  ike ipsec-policy ipsec_pol1
  enable
exit
```

```
security zone-pair public self
  rule 3
    description "ESP"
    action permit
    match protocol esp
    enable
  exit
  rule 4
    description "AH"
    action permit
    match protocol ah
    enable
  exit
exit
```

```
router ospf 1
  area 0.0.0.0
    enable
  exit
  enable
exit
```

```
tunnel gre 1
  ip ospf instance 1
  ip ospf
exit

interface gigabitethernet 1/0/2.100
  ip ospf instance 1
  ip ospf
exit

interface gigabitethernet 1/0/2.200
  ip ospf instance 1
  ip ospf
exit

interface gigabitethernet 1/0/2.300
  ip ospf instance 1
  ip ospf
exit
```

```
security zone-pair public self
  rule 5
    description "OSPF"
    action permit
    match protocol ospf
    enable
  exit
exit
```

Проверка 
```
sh ip ospf neighbors
```
```
sh ip route
```

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/c77249a2-eec9-4b23-9992-a10e891f4a68)

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/fa2b8166-cc1f-4d7d-a230-7c0f8f882e6c)

</details>

## 10.	[->](./10.md) На сервере SRV-HQ сконфигурируйте основной доменный контроллер на базе FreeIPA

a)	Создайте 30 пользователей user1-user30.  
b)	Пользователи user1-user10 должны входить в состав группы group1.  
c)	Пользователи user11-user20 должны входить в состав группы group2.  
d)	Пользователи user21-user30 должны входить в состав группы group3.  
e)	Разрешите аутентификацию с использованием доменных учетных данных на ВМ CLI-HQ.  
f)	Установите сертификат центра сертификации FreeIPA в качестве доверенного на обоих клиентских ПК.  

<details>
  <summary>ТЫКНИ</summary>

[->](./10.md)

</details>

# 11.	На SRV-BR сконфигурируйте proxy-сервер со следующими параметрами

a)	Пользователям group1 разрешен доступ на любые сервисы предприятия  
b)	Пользователям group2 разрешен доступ только к системе мониторинга  
c)	Пользователям group3 не разрешен доступ никуда, также, как и пользователям, не прошедшим аутентификацию  
d)	Любым пользователям компьютера CLI-HQ разрешен доступ в сеть Интернет и на все сервисы предприятия, кроме доменов vk.com, mail.yandex.ru и worldskills.org  
e)	Настройте клиент правого офиса на использование прокси сервера предприятия  
f)	Авторизация для proxy спрашивается браузером, SSO не ожидается  

| Запись | Тип записи |
|:-|:-|
|rtr-hq.company.prof|A|
|rtr-br.company.prof|A|
|sw-hq.company.prof|A|
|sw-br.company.prof|A|
|srv-hq.company.prof|A|
|srv-br.company.prof|A|
|cli-hq.company.prof|A|
|cli-br.company.prof|A|
|dbms.company.prof|CNAME|

<details>
  <summary>ТЫКНИ</summary>

Пока что нет

</details>

</details>
