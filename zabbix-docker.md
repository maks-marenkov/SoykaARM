ip link add link ens18 name ens18.300 type vlan id 300
ip link set dev ens18.300 up
ip addr add 10.0.10.66/27 dev ens18.300
ip route add 0.0.0.0/0 via 10.0.10.65
echo nameserver 8.8.8.8 > /etc/resolv.conf
Обновление пакетов и установка openvswitch:

apt-get update && apt-get install -y openvswitch
Автозагрузка:

systemctl enable --now openvswitch
ens18 - rtr-hq
ens19 - cicd-hq - vlan200 ens20 - srv-hq - vlan100 ens21 - cli-hq - vlan200

Создаем каталоги для ens19,ens20,ens21:

mkdir /etc/net/ifaces/ens{19,20,21}
Для моста:

mkdir /etc/net/ifaces/ovs0
Management интерфейс:

mkdir /etc/net/ifaces/mgmt
Не удалять настройки openvswitch:

sed -i "s/OVS_REMOVE=yes/OVS_REMOVE=no/g" /etc/net/ifaces/default/options
Мост /etc/net/ifaces/ovs0/options:

image

TYPE - тип интерфейса, bridge;
HOST - добавляемые интерфейсы в bridge.

mgmt /etc/net/ifaces/mgmt/options:

image

TYPE - тип интерфейса (internal);
BOOTPROTO - статически;
CONFIG_IPV4 - использовать ipv4;
BRIDGE - определяет к какому мосту необходимо добавить данный интерфейс;
VID - определяет принадлежность интерфейса к VLAN.

Поднимаем интерфейсы:

cp /etc/net/ifaces/ens18/options /etc/net/ifaces/ens19/options
cp /etc/net/ifaces/ens18/options /etc/net/ifaces/ens20/options
cp /etc/net/ifaces/ens18/options /etc/net/ifaces/ens21/options
Назначаем Ip, default gateway на mgmt:

echo 10.0.10.66/27 > /etc/net/ifaces/mgmt/ipv4address
echo default via 10.0.10.65 > /etc/net/ifaces/mgmt/ipv4route
Перезапуск network:

systemctl restart network
Проверка:

ip -c --br a
ovs-vsctl show
ens18 - rtr-hq делаем trunk и пропускаем VLANs:

ovs-vsctl set port ens18 trunk=100,200,300
ens19 - tag=200

ovs-vsctl set port ens19 tag=200
ens20 - tag=100:

ovs-vsctl set port ens20 tag=100
ens21 - tag=200

ovs-vsctl set port ens21 tag=200
Включаем инкапсулирование пакетов по 802.1q:

modprobe 8021q
