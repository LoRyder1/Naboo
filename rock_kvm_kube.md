rock_kvm_kube.md


July 27, 2025
ROCKY LINUX installed on Server

hostname: rocky-kube-host1
IP: 192.168.50.51
Gateway: 192.168.50.1
Router: 192.168.50.1

user: pnag
user: root


idrac: root: calvin

racadm set System.ServerOS.OSVersion "9.6"




nmcli connection show  # List all active connections

sudo nmcli connection delete enp1s0 # Replace enp1s0 with your actual connection name



sudo nmcli connection add type bridge con-name br0 ifname br0 \
    ipv4.method manual \
    ipv4.addresses <PowerEdge_Static_IP>/<Netmask_CIDR> \
    ipv4.gateway <Your_Router_IP> \
    ipv4.dns <Your_DNS_Server_IP> \
    connection.autoconnect yes

    sudo nmcli connection add type bridge con-name br0 ifname br0 \
    ipv4.method manual \
    ipv4.addresses 192.168.1.100/24 \
    ipv4.gateway 192.168.1.1 \
    ipv4.dns 8.8.8.8 \
    connection.autoconnect yes

sudo nmcli connection add type ethernet con-name enp1s0-slave ifname enp1s0 master br0 slave-type bridge connection.autoconnect yes