# Linux - How to add FireWall rule to Redhat Linux server

```bash
firewall-cmd --zone=public --add-port=25565/tcp --permanent
firewall-cmd --zone=public --add-port=25565/udp --permanent
firewall-cmd --reload
iptables-save | grep 25565
```
