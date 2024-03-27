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
