#!/usr/bin/python3

from mininet.net import Mininet
from mininet.node import Controller, OVSSwitch
from mininet.cli import CLI
from mininet.log import setLogLevel, info


def simple_tree_topology():
    net = Mininet(controller=Controller, switch=OVSSwitch)

    info("*** Adding controller\n")
    net.addController('c0')

    info("*** Adding switches\n")
    c1 = net.addSwitch('c1')

    a1 = net.addSwitch('a1')
    a2 = net.addSwitch('a2')

    e1 = net.addSwitch('e1')
    e2 = net.addSwitch('e2')
    e3 = net.addSwitch('e3')
    e4 = net.addSwitch('e4')

    info("*** Adding hosts\n")
    h1 = net.addHost('h1')
    h2 = net.addHost('h2')
    h3 = net.addHost('h3')
    h4 = net.addHost('h4')
    h5 = net.addHost('h5')
    h6 = net.addHost('h6')
    h7 = net.addHost('h7')
    h8 = net.addHost('h8')

    info("*** Creating links\n")
    net.addLink(c1, a1)
    net.addLink(c1, a2)

    net.addLink(a1, e1)
    net.addLink(a1, e2)
    net.addLink(a2, e3)
    net.addLink(a2, e4)

    net.addLink(e1, h1)
    net.addLink(e1, h2)
    net.addLink(e2, h3)
    net.addLink(e2, h4)
    net.addLink(e3, h5)
    net.addLink(e3, h6)
    net.addLink(e4, h7)
    net.addLink(e4, h8)

    info("*** Starting network\n")
    net.start()

    info("*** Displaying network connections\n")
    net.dump()

    info("*** Testing connectivity\n")
    net.pingAll()

    info("*** Running CLI\n")
    CLI(net)

    info("*** Stopping network\n")
    net.stop()


if __name__ == '__main__':
    setLogLevel('info')
    simple_tree_topology()
