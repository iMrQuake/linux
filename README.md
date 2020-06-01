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



