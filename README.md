# proxy-to-wireguard

自行修改`wireguard.ports`中`<snellport>`及`snell.environment.PSK`中`<password>`

wireguard配置文件命名为`wg0.conf`,`/root/ptwg/config`为目录，可自行修改

在wireguard配置文件`Interface`部分中加入以下内容
```
PostUp = ip rule add table 200 from $(ip addr show eth0 | grep "inet\b" | awk '{print $2}' | cut -d/ -f1)
PostUp = ip route add table 200 default via $(ip route | grep default | awk '{print $3}')
PreDown = ip rule delete table 200 from $(ip addr show eth0 | grep "inet\b" | awk '{print $2}' | cut -d/ -f1)
PreDown = ip route delete table 200 default via $(ip route | grep default | awk '{print $3}')
```