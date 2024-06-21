- Create the three pcs. 

kathara vstart --name pc1 --eth 0:A
kathara vstart --name pc2 --eth 0:B
kathara vstart --name pc3 --eth 0:C

- Create the switch 

kathara vstart --name switch --eth 0:A 1:B 2:C

- Assign the IPs

PC1: ip a add 192.168.3.1/12 dev eth0
PC2: ip a add 192.168.3.2/12 dev eth0
PC3: ip a add 192.168.3.3/12 dev eth0

- Configure bridge in switch. 

brctl addbr switch 
brctl addif switch eth0
brctl addif switch eth1
brctl addif switch eth2

- Start the bridge. 

ifconfig switch up (switch is the bridge name)

kathara lconfig -n wireshark --add A
docker run -d --name=wireshark --cap-add=NET_ADMIN --restart unless-stopped -p 3000:3000 lscr.io/linuxserver/wireshark:latest



ip route add default via 192.0.2.2 dev eth0