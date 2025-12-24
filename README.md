from mininet.net import Mininet
from mininet.node import OVSSwitch
from mininet.topo import Topo
from mininet.cli import CLI


class SimpleTreeTopo(Topo):
    def build(self):

        # Hosts
        h1 = self.addHost('h1')
        h2 = self.addHost('h2')
        h3 = self.addHost('h3')
        h4 = self.addHost('h4')
        h5 = self.addHost('h5')
        h6 = self.addHost('h6')
        h7 = self.addHost('h7')
        h8 = self.addHost('h8')

        # Switches
        s1 = self.addSwitch('s1')
        s2 = self.addSwitch('s2')
        s3 = self.addSwitch('s3')

        # Links
        self.addLink(s1, s2)
        self.addLink(s1, s3)

        self.addLink(s2, h1)
        self.addLink(s2, h2)
        self.addLink(s2, h3)
        self.addLink(s2, h4)

        self.addLink(s3, h5)
        self.addLink(s3, h6)
        self.addLink(s3, h7)
        self.addLink(s3, h8)


if __name__ == '__main__':
    topo = SimpleTreeTopo()

    # IMPORTANT PART — controller=None
    net = Mininet(topo=topo, controller=None, switch=OVSSwitch)
    net.start()

    CLI(net)
    net.stop()
