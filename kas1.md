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
interface fastethernet17
 loopback-detection enable 
 description PPPoE-17755
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
interface fastethernet18
 loopback-detection enable 
 description PPPoE-17869
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
interface fastethernet19
 loopback-detection enable 
 description FREE
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
interface fastethernet20
 loopback-detection enable 
 description PPPoE-17838
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
interface fastethernet21
 loopback-detection enable 
 description FREE
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
interface fastethernet22
 loopback-detection enable 
 description FREE
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
interface fastethernet23
 loopback-detection enable 
 description FREE
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
interface fastethernet24
 loopback-detection enable 
 description FREE
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
interface gigabitethernet1
 description 
 ip arp inspection trust 
 ip dhcp snooping trust 
 bridge multicast unregistered filtering 
 switchport trunk allowed vlan add 445,446,600,612-613 
!
interface gigabitethernet2
 description PPPoE-15864
 ip arp inspection trust 
 ip dhcp snooping trust 
 bridge multicast unregistered filtering 
 switchport trunk allowed vlan add 445,446,600,612-613 
!
interface gigabitethernet3
 description 
 ip arp inspection trust 
 ip dhcp snooping trust 
 bridge multicast unregistered filtering 
 switchport trunk allowed vlan add 445,446
!
interface gigabitethernet4
 description ""
 ip arp inspection trust 
 ip dhcp snooping trust 
 bridge multicast unregistered filtering 
 switchport trunk allowed vlan add 445,446
!
exit
ip igmp snooping vlan 3482 immediate-leave 
ip dhcp snooping 
ip dhcp snooping vlan 446 
ip default-gateway 10.5.194.193 
encrypted ip ssh-client key rsa key-pair
---- BEGIN SSH2 ENCRYPTED PRIVATE KEY ----
Comment: RSA Private Key
D6wAjEzztTS8NtPbBgNVxmHRj3USqup3xzTJSWRBKNbm6FaFwZx83LrGktJ0Gn+KakKBWY
FX0Ea4i0oDdhiUet90nevsczgVPWRbdOBdgcLSBbjfEPOpMt5vyoL3/xbdIqpWnSAPxiiy
CW7pIlU1v3CDC9stjLcJdrmxhErk7d6nhOSnqzzpKSXwbaePNC5byb4i/amTSzbBeryqwV
SWvhdWM6G1qLw2/s0xEBVMcLk4UK2mKwcyi/YkN3KvDEUw8QdQAs5fFFL6/aXNH3Fl6kNn
qZbjSik2ssBNiBAK4J+aHF8nH+jx8B9UB8pqqSwfDGjtuAolFOyCLW7JDD6E7gtmfvHAzL
ebSUioS96fMVDNF3ykFLfRtFiwK7xhf+WdeNisTSJBUtWAyOHCnU94ldOSBRswLYyl8yzm
7DnI4YAi1sXAbfKDsGsf1Ch/+mnCPG+eDZTK548/62IA4Wx1HHdx48msc4hSOhJAtIc5K2
zRC8F32ick8fVmgUkSP4wgTW3znG7vwZtU3KfEG9JioYmnkfqm9PAQGo8ymR/Il2uzsfj2
oE0+5XDPaGwm+UtJsK8FT18/D8tm3bG324av8C05z0Hd9nvMd73FrDESok/bIOKYLX99a9
i9rs0RGi/mo8hSUInBwPiNJJd+J6DdKrcr8XHRruYDyJxCi650Cb2M2k+V+/Dw1uUDv1YH
mIPjXy2CvO7jxyI3uYsJUWGUDjIEdomFjMm66ISvaxk7Qaj0agQQ7Yx8Hxp+J+21paB2K/
SOOoujot6taV+H3Ws/hHaKhtmz93DEu2/ouSUPvx5OoKmaaycTPtoOm9XoseX13BKLf3zy
hI+OFi2A6XmciYIm3SBBOG8qJy4vfiTZ1rI9lqwCYHgutv5Xy0S9A7nDN+avagdHDIOdWt
ifcRiYKs7JCgcrT7d6Tfb18V5H4S59bDvjCE1IcNuAgHr1X4hPy+gzS0o6lj1LZIpnd2qA
8uSYo9IXMfR4yElcnRtE5GOw2h4eEJvRh5QZs0dVDeAl/WwNfW7VXm4EMnUP/3CtN0/PK8
ZohOTmNsZr5AdOF3ZID01diDT/2JEoMLsvir1Tf6Py3rsf1eG45cvLUjhOyQ==
---- END SSH2 PRIVATE KEY ----

---- BEGIN SSH2 PUBLIC KEY ----
Comment: RSA Public Key
AAAAB3NzaC1yc2EAAAADAQABAAAAgQCeXwIbXofpAfqMScuxOMquGx1dPXcckIbi7SWWyw
7FUjUKg88glJF2GQcXTZhanjwHonD0ZVZDth+505i2fvLGROWMu3Kf9tnff4M88ki78qDl
cRIX5dp31AdeXdCKNMuBOtF5PaDRVpWyTQgvRpBdmoz8w+93oNKpRpGcq8mYPQ==
---- END SSH2 PUBLIC KEY ----
.
encrypted ip ssh-client key dsa key-pair
---- BEGIN SSH2 ENCRYPTED PRIVATE KEY ----
Comment: DSA Private Key
AQolxJryr+dbMbws7JbZA71uIenDeuzKSTlf6os/Z//mJ6eAOwmY0pCUTk2YGUqkK5LbR0
oPj6BkRxvm29fsGxysMc9yn6fyApacteDS7TswAShd/lYrDWkOX3cPiBrbX60d/mAerX4S
uZ/9S4XC6niPlNpZrCnuJrML+HLvItLY3GihfkYzn3NmWN9gzJIZ4dx4/xiG4862In6PnN
I7x+BgqmFQXlLHakeZwh2ybbPrc9d3lQtX6O+CWsFyLAS+T1cr5kCrC14fv2rM1tGMBuPz
KS64FeZ2F47aMyXC6WyntC7KTYUwbpP9uo0ib49HW6oi3ES9xcMbZvBwkIWxfOW1/nghNi
EB1hoxrG9ucCCH+jiESVBHqx2b6rTzrIFJ5yDhjRspe/QTm+jGsOxkxo7V2yX3UuZxdq1q
qhRNBx10xUtzvepzWaKSKP9zUzRJELpEUGcG51xsKcpugQOC9B7WRSAjE14kZgvYuz7r/U
Z5m4wu/ODPInH6fA8ojLEx+Gsp1b+LL2Ufq8qa/E/NFN0nJuNafmmTIbCE5exAdcP/82oK
r52r7j/bbArRsU3txDVDvRjA0tW/rFn6HlNu2w1sCdyg3+hOdVcF4Dd1ZA/prcs7srHIbN
xD2UMW4OQhxi1EGPAYW0gbl6jhMnkkU62zvGoabiqgxiga+giVigBIgzPBczYMO+HiaORv
ETmS3A/IGcXZlTiyKQnLXzy4Qvy7C+vu4rVSGMgTNtlDoVm0K7DmwkP89pyCYabOp/NvnK
OuThxsV7o7naSw9eY8AJC6vL2iPqo0IdmTGOGNYRR+1siDCS61YqCQOriSy6Ws
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

</details>
I+HKlHVzJc2FPTCsV3s+7uQXXhBoEBO2aEC9gRtJQymgrkc/AU5ZQ16DHOuEIbmLMHD
o15wbYxldiZHy8eDAfucFwpYqr8LihD0Hwg670J5TZU01wv5ZhFOpG6ESEFfIDWHIagJyw
cpXYH+JTKM1rlPujEE8pl9M3CRMSOHP3TjUkwbiUIuo7v/DXqHl2XF9TPvCIDfLAmYfl++
F3/ZWj+zT0LHGJtmeOZm/t2vuijNFPh3tpyuitnP1zfasrKTA3PUR9NToNsT+pRjxQAfKd
F5u0Uf0SQfazWsSJBIbjQIFb0GAJy6D4JvxxzRA638nMtp01zdrZhPOMi7U9Om3HcR1p8E
C3OR94zSjq+aTUx7fhiNyfhE4melB62IJHwgL+IOQU3WgvezOSqDFtvEg7mYc4SzskOnfj
4PU3pwOpU6KFYj2zZO78ognbsdolU1xfCN6UJAGbKFujCdWXGQRYNDUAQGag==
---- END SSH2 PRIVATE KEY ----

---- BEGIN SSH2 PUBLIC KEY ----
Comment: RSA Public Key
AAAAB3NzaC1yc2EAAAADAQABAAAAgQDPHTB+ro8Uj9phX6K2lbeymR6WMJkIsqLvxbBGAX
jbH5+cSTaB2fy6lqgpsrLBxDcWEksNrZIUMbtbKq2WXk4rtZUJvG5lGhWjzAfKvx+dCdNU
Yw2UTtHz4DhPmXQZ7sUunsAltBWGiKUmXiY7WBJMUvzspjNdv5UgPHFJacjIXQ==
---- END SSH2 PUBLIC KEY ----
.
encrypted crypto key import dsa
---- BEGIN SSH2 ENCRYPTED PRIVATE KEY ----
Comment: DSA Private Key
A/rauF5w297xMVuC4c5v3snsBd8Hju/SOBcB46oHSOYC7SsDAZXmju6RSKnL4W/xO0HuVz
chJdmak87dIQtobp3iD9dnpvG+707SW+NtiTCLH+0dS+IF5FjsEMA+uIOxziIBC7ouo4M+
XKDBpsIse0qq1Dfxk8W757XQtSEiRcsESaNpW7/k076jvuPkUL5zUknpRI1WDHf0CO8egC
P2zUu+KPdSrHKBMnMI3EAnhYGBZhmIF3phrxkUfd03YLIS/qchGDpXkGrZ6rSixjYs9OH0
WjxcGGyQsgCqc6oXms9i8+qMr04K00AO+Kn62BXlq021nAB8Sv078gicS3HizBkSNhyEPA
GKzhfpt7fhG2/wNjtoogY4SdmALuXb0CwEWC+Bv3D1KOCEbJzAsecfs+Ry1djoXB7zfOSG
3cXasa68UQRu+FO3qZnfI2Xp/iYkzU3j6f3MGLBA66u4iEWARCXM8Cn2iVy1/ILvuw8qEn
Vt5uFLKOgOM1uh+nLA0ailHtnDfJR6A4Nnbj9nVW1nrYuEaGe9SXHINLQBl7AJGmtDWnZ4
HDJVxtMnOT6Gu/Usd0LG5CWBh7cIA0ULDar2jxG60zkbxRiuKNLJB0LFeTd122Dlw5a2sv
YlcT5o8LGsNG3GBFh9aBJivaeKpAgEUnU43R+IsADDwJCr7nPrm7LMKndG58nUrZ6l+v51
5E37vdmbEvNN1ptlVVd2flPeZBnNaPao2RASVeBQWSvmNxRT8UEOPBLu57SBEDgurcR+GQ
j6IcuTGJoi36Fu1YaS+MWqRn9k3wZKNTBDbGnC7W3X96ziIB1tfvQ+d8HGW+P9
---- END SSH2 PRIVATE KEY ----

---- BEGIN SSH2 PUBLIC KEY ----
Comment: DSA Public Key
AAAAB3NzaC1kc3MAAACBALrBVQncH0ItzZ2iJ5qqHFV7L9gRtREBpmufRcQTT+ybRicoYD
Hx08iQ7nJQbeiIYJ+aajtqSz7s2cx0VM/w7cZ4m58HkkQeaCAT9adSebpCGTvTDvXBbUau
pBnjFrAibn9e1JhWiC5fR/Zj+MOrffeqslDbsL/sPgruK3EXJr8zAAAAFQC+vtbLwhVtgQ
zd8eLjFnbvUgeSFQAAAIAwt0+mrl3rKnYkjADO7z7+lkAhG/LT1WN0QI7pNLjE6Y4wQc9s
FHgW+reUUMImLsXYOoHe2m26dwo/BTGWETs3nc4B6yldB1vp23Q8rr49+2JvvNzeGGoOb0
lCAhf0/lfox3wFtVBg8nHYhfdvHCzmmJdLW/k6dedZ6dGcjS93EAAAAIBOiFiAji5mL/uq
dapdfHplnYxaj+hfp8XeMgDRhn1MAKmvh2J6uGlmMfCk7GWf5nphAV7qnqAwffJaX8Yf8T
RyrcqZGGBRgVl7/2W2gCn4cLOhoWkSoeW9GL1qfbzG0DyfP75ELqdAfGoyTDS7UunZoIxD
tHbmOV5QUkmsDVDbTw==
---- END SSH2 PUBLIC KEY ----
.
encrypted crypto certificate 1 import
-----BEGIN RSA ENCRYPTED PRIVATE KEY-----
hB7dGIjz6W+dppJqNSV1o+9c0/Gre95e6JpfauH8ySdP70sLaYOIdXInCL1EdiZ3Nbqe8Z
IQIiWD/5wk5Fi2p87mzx1MP+B+xHiyTHL0Rlwh6fmqEhNYa4YmgDDXeY2rew8AmWoFD7C1
sumg0VeiIQ9bteyWLtB2vdmQ6FSZT7L3swgAy40eVZsHYLIewGjf7tX3B2a62PqswZTPIw
fOwSgL08GdO9bATFnq1qx6pJYkGjJA+6dd6KZMs66XY6Fvb4JET9y5/JLBLRESgBvxWjpC
3XCERvb0oJ6PtWMAciYDtGTneX0pK+JJsp/BtT4Xyqp0QYuyRRB6bAMpk0pa7gla139k/k
womHfIqboNVFjnba5wGQUhaVIh9mm2NzlNiNmENa6ue7feF6usctld+lq7SqofK4amDME5
+DHNXW2SCdj/3+XhevYFeypbcCAsWgysBU7Ua2p5Ac+KYuHydoCZBFQzkY1rNtryNdMMKe
7fc3uL+DABiRoth1PNRPLFREMrEPt5feQpiDMhc0zsmvcOKsnMcXESWq+vxS4NKsQs3SGf
ZFJKqhty4e4llylsaOp8sUfsB4GDNUCZY0Tke2eEaG1ynbJK+FKwr52mSI8WaXCP7g+HPQ
bOHJe08fV6RCMey2d+DbN4L+Rnpmcr4Ns6lmloPWGv4cBx6CYVhfDmq6RGcsq71FjlDDDn
GorUqcyHKF3m1D6PnYVf/vrX70JZFnW9PZgdn5M4QDJSgynuYcae3vP95hXUBOiSJ2xnor
8GrXXckN3xWgIG2fHh66rDA6xKBFKvwDBDDvInnv/cLcEnKrT9udmEvhmSnx64mgyvidbg
5DOPbyfbz4oJ++49Hmmfo7UHEllzdlhL0y/qq0z2cQQ+qQKYWWODzIdoUQ3Bu1Qj/KSrir
n8jWcOO7GTitYxNfss6CV8+KOC813KkEm6eR643SEuALlhCpNh2wmSwGJ/Y5mdlpkBEl5i
VTrHfUlXwFhZUjRBllSya/XvCtR+MZHKjmAzhFm9ja2JK9E0+VMIyqA4nBoxCMzPUyojL+
/zlftJAU/+8nzUXHVgZ0qc2b5UJvHO+c65SJNi6oeehdqvJ5zxuKPM23dwAQ==
-----END RSA PRIVATE KEY-----

-----BEGIN RSA PUBLIC KEY-----
MIGJAoGBAORC9H9GeKASUYrTU/fguACojEjpRA7fcX5N07Vp4scjiOgyewintrgb4Hie6I
DspqlIPZ3GdKtp1ae+yRqN6HtoHR6ekIe+CLgzZjvT/NFMqGiFFbvrVGpiUZomgDbUP+4U
R5ccN1i1uVt7rFBARFz7qTEuie1O+Bo00B7QpqgNAgMBAAE=
-----END RSA PUBLIC KEY-----
-----BEGIN CERTIFICATE-----
MIICIjCCAYsCEHQDXV4ghGAmn1Z1NOjWFQQwDQYJKoZIhvcNAQEFBQAwUjELMAkG
A1UEBhMCICAxCjAIBgNVBAgTASAxCjAIBgNVBAcTASAxEzARBgNVBAMTCjEwLjUu
MTMwLjIxCjAIBgNVBAoTASAxCjAIBgNVBAsTASAwHhcNMTQwODA2MTY1NjQzWhcN
MTUwODA2MTY1NjQzWjBSMQswCQYDVQQGEwIgIDEKMAgGA1UECBMBIDEKMAgGA1UE
BxMBIDETMBEGA1UEAxMKMTAuNS4xMzAuMjEKMAgGA1UEChMBIDEKMAgGA1UECxMB
IDCBnzANBgkqhkiG9w0BAQEFAAOBjQAwgYkCgYEA5EL0f0Z4oBJRitNT9+C4AKiM
SOlEDt9xfk3TtWnixyOI6DJ7CKe2uBvgeJ7ogOymqUg9ncZ0q2nVp77JGo3oe2gd
Hp6Qh74IuDNmO9P80UyoaIUVu+tUamJRmiaANtQ/7hRHlxw3WLW5W3usUEBEXPup
MS6J7U74GjTQHtCmqA0CAwEAATANBgkqhkiG9w0BAQUFAAOBgQDeLfUUNR8pCdXK
33Ka7pRXszTLvHccFchBlyHbeIVjgmp0Q2G0oiuv6vCheQ0KFi4GHMXOnrqm3KR4
HJb1ANAZ4H+1NgZQJruQ/GoWPH5+xt3uSsZnY8s9JzjAz5VFcXoMyJPz8i9Vuas/
btotEOVRWQucyeOWJdd6EMUZI17tSw==
-----END CERTIFICATE-----
.
