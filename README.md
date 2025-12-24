from mininet.net import Mininet
from mininet.node import OVSBridge
from mininet.topo import Topo
from mininet.cli import CLI


class SimpleTreeTopo(Topo):
    def build(self):

        # Hosts
        hosts = []
        for i in range(1, 9):
            hosts.append(self.addHost(f'h{i}'))

        # Switches
        s1 = self.addSwitch('s1')
        s2 = self.addSwitch('s2')
        s3 = self.addSwitch('s3')

        # Core links
        self.addLink(s1, s2)
        self.addLink(s1, s3)

        # Access links
        for h in hosts[:4]:
            self.addLink(s2, h)

        for h in hosts[4:]:
            self.addLink(s3, h)


if __name__ == '__main__':
    topo = SimpleTreeTopo()
    net = Mininet(topo=topo, switch=OVSBridge)
    net.start()
    CLI(net)
    net.stop()
