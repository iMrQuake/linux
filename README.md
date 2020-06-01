# linux

# Disable IPV6 and Enable IPV4 forwarding
## With sysctl.conf
`su - root`

`nano /etc/sysctl.conf`

`net.ipv4.ip_forward=1`

`sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1`

`sudo sysctl -w net.ipv6.conf.default.disable_ipv6=1`

`sudo sysctl -w net.ipv6.conf.lo.disable_ipv6=1`

`sudo sysctl -p`

## With grub
`nano  /etc/default/grub`

`GRUB_CMDLINE_LINUX_DEFAULT="quiet splash ipv6.disable=1"`

`GRUB_CMDLINE_LINUX="ipv6.disable=1"`

`update-grub`

## Check with
```ip a```

## IPV4 forwarding for UFW
`nano /etc/default/ufw.conf`
`DEFAULT_FORWARD_POLICY="ACCEPT"`

# Get openvpn
apt install network-manager-openvpn-gnome network-manager-openvpn gadmin-openvpn-client net-tools

# Firewall
## Prepare firewall
```
ufw status numbered
ufw enable
```
```
ufw default deny incoming
```
```
ufw default deny outgoing
```
```
ufw allow out on tun0 'comment allow any out on tun0 i.e. VPN'
```
```
ufw allow out on eth0 log to 10.0.2.0/24 'comment local_network'
```
## repeat for each VPN server/port/proto
```
sudo ufw allow out log from any to VPN_IP port VPN_PORT proto VPN_PROTO comment 'allow VPN server IP to be reach to establish connection'
sudo ufw allow out log from any to 172.94.102.4 comment 'ivacy denmark'
sudo ufw allow out log from any to 172.94.12.4  comment 'ivacy germany'
sudo ufw allow out log from any to 194.242.195.227  comment 'ivacy luxembourg'
sudo ufw allow out log from any to 188.72.98.4  comment 'ivacy netherlands'
sudo ufw allow out log from any to 172.111.246.4  comment 'ivacy sweden'
```
## VPN connection should work
check with https://www.dnsleaktest.com and check DNS are the one from the VPN provider not from your ISP


