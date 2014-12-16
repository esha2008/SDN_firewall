SDN_firewall
============

Firewall application implemented in a software defined network, using mininet and python.

A small network is set up in mininet-vm that contains 6 switches, each having a host, using the following code(which I've saved in file esha-topo.py):


This topology code is placed in the /home/mininet/mininet/custom

Now, run the POX controller on a separate SSH connection along with the firewall module, using the following command:
./pox.py forwarding.l2_learning openflow.discovery openflow.spanning_tree --no-flood --hold-down pox.misc.firewall
while being in /pox directory.

Then, execute the mininet network on the first window, while being in /home/mininet/mininet/custom working directory.Use the following code:
mn --custom esha-topo.py --topo mytopo --mac --controller=remote,ip=127.0.0.1,port=6633
Exexute pingall and the host having ip_0 will not reach host with ip_1 , according to the firewallpolicies.csv.
