spanning-tree mode mstp
ip igmp snooping
ip arp inspection 
port jumbo-frame
bridge multicast filtering
vlan database
vlan 587,687
exit





interface range ethernet g(1-4)
switchport mode trunk
switchport trunk allowed vlan add all
ip arp inspection trust
ip dhcp snooping trust 
exit
interface range ethernet e(1-24)
port storm-control broadcast enable
spanning-tree portfast auto
spanning-tree guard root
switchport mode access
switchport access vlan 587
no sh
exit

interface vlan 687
ip igmp snooping
name CUST
exit

interface vlan 587
ip address 10.5.34.200 255.255.255.224
name MGMT
exit

port storm-control unknown-unicast fastethernet enable

ip default-gateway 10.5.34.193
ip dhcp relay address 10.5.0.4
ip dhcp relay address 10.5.0.29
ip dhcp relay enable

mac access-list pppoe_cl_686
permit any ff:ff:ff:ff:ff:ff 00:00:00:00:00:00 vlan 688 ethtype 8863
permit any 00:0c:29:6d:91:43 00:00:00:00:00:00 vlan 688 ethtype 8863
permit any 00:0c:29:6d:91:43 00:00:00:00:00:00 vlan 688 ethtype 8864
deny any any vlan <details><summary>688</summary>

```
apt-get update && apt-get install -y haveged
```

```
systemctl enable --now haveged
```

```
apt-get install -y freeipa-server
```

```
ipa-server-install
```

```
kinit admin
```

```
for i in {1..30};do 
	echo "P@ssw0rd" | ipa user-add user$i --first=User --last=$i --password;
	ipa user-mod user$i --setattr=krbPasswordExpiration=20251225011529Z;
done
```

```
for i in {1..3}; do
	ipa group-add group$i;
done
```

```
for i in {1..10}; do
	ipa group-add-member group1 --users=user$i;
done
```


```
for i in {11..20}; do
	ipa group-add-member group2 --users=user$i;
done
```

```
for i in {21..30}; do
	ipa group-add-member group3 --users=user$i;
done
```

```
cp /etc/ipa/ca.crt /etc/pki/ca-trust/source/anchors/
```
```
update-ca-trust extract
```


```
apt-get update && apt-get install -y freeipa-client zip
```


```
ipa-client-install --mkhomedir
```

```
cp /etc/ipa/ca.crt /etc/pki/ca-trust/source/anchors/
```
```
update-ca-trust extract
```

</details>
ethtype 8863
deny any any vlan 688 ethtype 8864
deny any any vlan 688 ethtype 86dd
deny disable-port any 01:80:c2:00:00:00 00:00:00:00:00:00
permit any any
exit
mac access-list pppoe_cl
permit any ff:ff:ff:ff:ff:ff 00:00:00:00:00:00 vlan 687 ethtype 8863
permit any 00:0c:29:6d:91:43 00:00:00:00:00:00 vlan 687 ethtype 8863
permit any 00:0c:29:6d:91:43 00:00:00:00:00:00 vlan 687 ethtype 8864
deny any any vlan 687 ethtype 8863
deny any any vlan 687 ethtype 8864
deny any any vlan 687 ethtype 86dd
deny disable-port any 01:80:c2:00:00:00 00:00:00:00:00:00
permit any any



