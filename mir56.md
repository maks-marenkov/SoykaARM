interface fastethernet11
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
interface fastethernet12
 loopback-detection enable 
 description 19853
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
interface fastethernet13
 loopback-detection enable 
 description PPPoE-13753
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
interface fastethernet14
 loopback-detection enable 
 description PPPoE-15329
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
interface fastethernet15
 loopback-detection enable 
 description PPPoE-15864
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
interface fastethernet16
 loopback-detection enable 
 description PPPoE-17567
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
<details>
  <summary>5</summary>

rtr-hq:
```
config
security zone public
exit
int te1/0/2
security-zone public
exit
object-group network COMPANY
ip address-range 10.0.10.1-10.0.10.254
exit
object-group network WAN
ip address-range 11.11.11.11
exit
nat source
pool WAN
ip address-range 11.11.11.11
exit
ruleset SNAT
to zone public
rule 1
match source-address COMPANY
action source-nat pool WAN
enable
exit
exit
commit
confirm

```
rtr-br:
```
config
security zone public
exit
int te1/0/2
security-zone public
exit
object-group network COMPANY
ip address-range 10.0.20.1-10.0.20.254
exit
object-group network WAN
ip address-range 22.22.22.22
exit
nat source
pool WAN
ip address-range 22.22.22.22
exit
ruleset SNAT
to zone public
rule 1
match source-address COMPANY
action source-nat pool WAN
enable
exit
exit
commit
confirm

```

</details>
username ctadmin password 876236195ba5d55f1c4e4ae7faa074ae level 15 encrypted
snmp-server location "Armavir, Izobilnaya, 1 [45.005550219507974, 41.04266276425468]"
snmp-server contact noc@city-telekom.ru
snmp-server community public ro 10.5.0.11 view Default 
snmp-server community t0LmsCrRxU ro 10.5.0.9 view Default 
snmp-server host 10.5.0.11 public traps 2 
no ip http server
no ip https server
clock timezone +3 zone MSK
sntp client enable vlan 587
clock source sntp
sntp unicast client enable
sntp unicast client poll
sntp anycast client enable
sntp broadcast client enable
sntp server 10.5.0.4 poll
sntp server 10.5.0.29 poll
<details>
  <summary>6</summary>

```
configure terminal
ip dhcp-server pool COMPANY-HQ
network 10.0.10.32/27
default-lease-time 3:00:00
address-range 10.0.10.33-10.0.10.62
excluded-address-range 10.0.10.33                      
default-router 10.0.10.33 
dns-server 10.0.10.2
domain-name company.prof
exit
```

```
ip dhcp-server
```


</details>
ncrypted ip ssh-client key rsa key-pair
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
