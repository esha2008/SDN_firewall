SDN_firewall
============

Firewall application implemented in a software defined network, using mininet and python.

A small network is set up in mininet-vm that contains 6 switches, each having a host, using the following code(which I've saved in file esha-topo.py):

from mininet.topo import Topo

class MyTopo( Topo ):
    "Simple topology example created by me."

    def __init__( self ):
        "Create custom topo."

        # Initialize topology
        Topo.__init__( self )

        # Add hosts and switches
        FirstHost = self.addHost( 'h1' )
        SecondHost = self.addHost( 'h2' )
        ThirdHost = self.addHost( 'h3' )
        FourthHost = self.addHost( 'h4' )
        FifthHost = self.addHost( 'h5' )
        SixthHost = self.addHost( 'h6' )
        firstSwitch = self.addSwitch( 's1' )
        secondSwitch = self.addSwitch( 's2' )
        thirdSwitch = self.addSwitch( 's3' )
        fourthSwitch = self.addSwitch( 's4' )
        fifthSwitch = self.addSwitch( 's5' )
        sixthSwitch = self.addSwitch( 's6' )

        # Add links
        self.addLink( firstSwitch, FirstHost )
        self.addLink( secondSwitch, SecondHost )
        self.addLink( thirdSwitch, ThirdHost )
        self.addLink( fourthSwitch, FourthHost )
        self.addLink( fifthSwitch, FifthHost )
        self.addLink( sixthSwitch, SixthHost )
        self.addLink( firstSwitch, secondSwitch  )
        self.addLink( secondSwitch, thirdSwitch )
        self.addLink( thirdSwitch, sixthSwitch )
        self.addLink( fourthSwitch, sixthSwitch )
        self.addLink( fourthSwitch, thirdSwitch )
        self.addLink( firstSwitch, fourthSwitch )
        self.addLink( firstSwitch, fifthSwitch )
        self.addLink( secondSwitch, fifthSwitch )
        self.addLink( secondSwitch, sixthSwitch )
        self.addLink( fifthSwitch, thirdSwitch )

topos = { 'mytopo': ( lambda: MyTopo() ) }
This topology code is placed in the /home/mininet/mininet/custom

Now, run the POX controller on a separate SSH connection along with the firewall module, using the following command:
./pox.py forwarding.l2_learning openflow.discovery openflow.spanning_tree --no-flood --hold-down pox.misc.firewall
while being in /pox directory.

Then, execute the mininet network on the first window, while being in /home/mininet/mininet/custom working directory.Use the following code:
mn --custom esha-topo.py --topo mytopo --mac --controller=remote,ip=127.0.0.1,port=6633
Exexute pingall and the host having ip_0 will not reach host with ip_1 , according to the firewallpolicies.csv.
