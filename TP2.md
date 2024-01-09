**vérifier la bonne installatation**
```
az>> az group create --name efreitp2 --location francecentral
{
  "id": "/subscriptions/43a3cde7-d2e2-42de-81fb-c7465d02bdd1/resourceGroups/efreitp2",
  "location": "francecentral",
  "managedBy": null,
  "name": "efreitp2",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
```
**Partie 1 : Premiers pas Azure**
**I. Premiers pas**

*Créez une VM depuis la WebUI*
```
MacBook-Pro-de-MBP-2015:~ MBP-2015$ ssh lawerz@4.231.239.250
The authenticity of host '4.231.239.250 (4.231.239.250)' can't be established.
ED25519 key fingerprint is SHA256:B/X4J7FwNdt34UpM6ujnDCq6P9ortKwOVryVPnI92UA.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '4.231.239.250' (ED25519) to the list of known hosts.
Welcome to Ubuntu 22.04.3 LTS (GNU/Linux 6.2.0-1018-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Tue Jan  9 13:58:48 UTC 2024

  System load:  0.193359375       Processes:             104
  Usage of /:   5.1% of 28.89GB   Users logged in:       0
  Memory usage: 32%               IPv4 address for eth0: 10.0.0.4
  Swap usage:   0%

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.
```
*Créez une VM depuis le Azure CLI*
```
az>> vm create --name toto  --resource-group VMAZ --image Ubuntu2204 --admin-username lawerz --ssh-key-values "/Users/MBP-2015/.ssh/id_rsa.pub"
{
  "fqdns": "",
  "id": "/subscriptions/43a3cde7-d2e2-42de-81fb-c7465d02bdd1/resourceGroups/VMAZ/providers/Microsoft.Compute/virtualMachines/toto",
  "location": "northeurope",
  "macAddress": "00-0D-3A-BA-A4-07",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.6",
  "publicIpAddress": "104.41.217.113",
  "resourceGroup": "VMAZ",
  "zones": ""
}
```
```
MacBook-Pro-de-MBP-2015:~ MBP-2015$ ssh lawerz@104.41.217.113
The authenticity of host '104.41.217.113 (104.41.217.113)' can't be established.
ED25519 key fingerprint is SHA256:9qR7a/XxVF3aKu03Cn0liJwO8ZjUA0U25uNqcNZitFo.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '104.41.217.113' (ED25519) to the list of known hosts.
Welcome to Ubuntu 22.04.3 LTS (GNU/Linux 6.2.0-1018-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Tue Jan  9 14:57:58 UTC 2024

  System load:  0.00390625        Processes:             99
  Usage of /:   5.1% of 28.89GB   Users logged in:       0
  Memory usage: 8%                IPv4 address for eth0: 10.0.0.6
  Swap usage:   0%

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.
```
*Créez deux VMs depuis le Azure CLI*

```
az>> vm create --name tata --resource-group VMAZ --image Ubuntu2204 --admin-username lawerz --ssh-key-values "/Users/MBP-2015/.ssh/id_rsa.pub"
{
  "fqdns": "",
  "id": "/subscriptions/43a3cde7-d2e2-42de-81fb-c7465d02bdd1/resourceGroups/VMAZ/providers/Microsoft.Compute/virtualMachines/tata",
  "location": "northeurope",
  "macAddress": "00-0D-3A-65-AC-F8",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "20.238.45.68",
  "resourceGroup": "VMAZ",
  "zones": ""
}
```
```
az>> vm create --name toto  --resource-group VMAZ --image Ubuntu2204 --admin-username lawerz --ssh-key-values "/Users/MBP-2015/.ssh/id_rsa.pub"
{
  "fqdns": "",
  "id": "/subscriptions/43a3cde7-d2e2-42de-81fb-c7465d02bdd1/resourceGroups/VMAZ/providers/Microsoft.Compute/virtualMachines/toto",
  "location": "northeurope",
  "macAddress": "00-0D-3A-BA-A4-07",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.6",
  "publicIpAddress": "104.41.217.113",
  "resourceGroup": "VMAZ",
  "zones": ""
}
```
*Ping entre les machines*
```
lawerz@tata:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:0d:3a:65:ac:f8 brd ff:ff:ff:ff:ff:ff
    inet 10.0.0.4/24 metric 100 brd 10.0.0.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::20d:3aff:fe65:acf8/64 scope link 
       valid_lft forever preferred_lft forever
lawerz@tata:~$ ping 10.0.0.6
PING 10.0.0.6 (10.0.0.6) 56(84) bytes of data.
64 bytes from 10.0.0.6: icmp_seq=1 ttl=64 time=1.06 ms
64 bytes from 10.0.0.6: icmp_seq=2 ttl=64 time=1.17 ms
64 bytes from 10.0.0.6: icmp_seq=3 ttl=64 time=0.981 ms
64 bytes from 10.0.0.6: icmp_seq=4 ttl=64 time=1.05 ms
^C
--- 10.0.0.6 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 0.981/1.063/1.165/0.065 ms
```
```
lawerz@toto:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:0d:3a:ba:a4:07 brd ff:ff:ff:ff:ff:ff
    inet 10.0.0.6/24 metric 100 brd 10.0.0.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::20d:3aff:feba:a407/64 scope link 
       valid_lft forever preferred_lft forever
lawerz@toto:~$ ping 10.0.0.4
PING 10.0.0.4 (10.0.0.4) 56(84) bytes of data.
64 bytes from 10.0.0.4: icmp_seq=1 ttl=64 time=2.01 ms
64 bytes from 10.0.0.4: icmp_seq=2 ttl=64 time=1.19 ms
64 bytes from 10.0.0.4: icmp_seq=3 ttl=64 time=1.17 ms
64 bytes from 10.0.0.4: icmp_seq=4 ttl=64 time=1.40 ms
^C
--- 10.0.0.4 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 1.172/1.445/2.014/0.340 ms
```
*Tester cloud-init*
```
vm create --name tatata --resource-group VMAZ --image Ubuntu2204 --admin-username lawerz --ssh-key-values "/Users/MBP-2015/.ssh/id_rsa.pub" --custom-data /Us
{
  "fqdns": "",
  "id": "/subscriptions/43a3cde7-d2e2-42de-81fb-c7465d02bdd1/resourceGroups/VMAZ/providers/Microsoft.Compute/virtualMachines/tatata",
  "location": "northeurope",
  "macAddress": "00-0D-3A-B6-AB-87",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "20.223.239.176",
  "resourceGroup": "VMAZ",
  "zones": ""
}
```
*Vérifier que cloud-init a bien fonctionné*
```













