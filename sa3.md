sd-control-start 
ssd config 
ssd file passphrase control unrestricted 
no ssd file integrity control 
ssd-control-end cb0a3fdb1f3a1af4e4430033719968c0 
!
spanning-tree mode mst
port jumbo-frame
bridge multicast filtering 
vlan database
vlan 445,446,600,612-613 
exit
voice vlan oui-table add 0001e3 Siemens_AG_phone________
voice vlan oui-table add 00036b Cisco_phone_____________
voice vlan oui-table add 00096e <details>
  <summary>Avaya___________________</summary>


```
ip link add link ens18 name ens18.300 type vlan id 300
ip link set dev ens18.300 up
ip addr add 10.0.10.66/27 dev ens18.300
ip route add 0.0.0.0/0 via 10.0.10.65
echo nameserver 8.8.8.8 > /etc/resolv.conf
apt-get update && apt-get install -y openvswitch
```

```
systemctl enable --now openvswitch
```

```
mkdir /etc/net/ifaces/ens{19,20,21}
```

```
mkdir /etc/net/ifaces/ovs0
```

```
mkdir /etc/net/ifaces/mgmt
```

```
sed -i "s/OVS_REMOVE=yes/OVS_REMOVE=no/g" /etc/net/ifaces/default/options
```
Мост `/etc/net/ifaces/ovs0/options`:

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/6b3421b9-9260-47d7-a61e-a3ded4399557)


mgmt `/etc/net/ifaces/mgmt/options`:

![image](https://github.com/abdurrah1m/Professionals_2024/assets/148451230/8720b7e7-dd56-4116-aa44-13e586f31c70)


```
cp /etc/net/ifaces/ens18/options /etc/net/ifaces/ens19/options
cp /etc/net/ifaces/ens18/options /etc/net/ifaces/ens20/options
cp /etc/net/ifaces/ens18/options /etc/net/ifaces/ens21/options
```

```
echo 10.0.10.66/27 > /etc/net/ifaces/mgmt/ipv4address
```
```
echo default via 10.0.10.65 > /etc/net/ifaces/mgmt/ipv4route
```

```
systemctl restart network
```

```
ip -c --br a
```
```
ovs-vsctl show
```

```
ovs-vsctl set port ens18 trunk=100,200,300
```

```
ovs-vsctl set port ens19 tag=200
```

```
ovs-vsctl set port ens20 tag=100
```

```
ovs-vsctl set port ens21 tag=200
```

```
modprobe 8021q
```
</details>

voice vlan oui-table add 000fe2 H3C_Aolynk______________
voice vlan oui-table add 0060b9 Philips_and_NEC_AG_phone
voice vlan oui-table add 00d01e Pingtel_phone___________
voice vlan oui-table add 00e075 Polycom/Veritel_phone___
voice vlan oui-table add 00e0bb 3Com_phone______________
loopback-detection enable
green-ethernet energy-detect
ip dhcp relay address 10.5.0.4
ip dhcp relay address 10.5.0.29
ip dhcp relay enable
qos advanced 
mac access-list extended pppoe_cl
permit any ff:ff:ff:ff:ff:ff 00:00:00:00:00:00 vlan 481 8863 0000 ace-priority 1
permit any 00:0c:29:6d:91:43 00:00:00:00:00:00 vlan 481 8863 0000 ace-priority 2
