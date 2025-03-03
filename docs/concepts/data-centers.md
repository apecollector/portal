# Decentralized Data Centers

The Internet Computer blockchain is not physical hardware that exists in any physical location. Instead, the Internet Computer blockchain combines computing resources provided by independently-operated data centers around the world.

Unlike a public or private cloud, the Internet Computer blockchain is not owned and operated by a single private company. Instead, the Internet Computer blockchain is a public utility with updates and operations that are managed through an algorithmic, decentralized governance system defined in the protocol. Its architecture enables multiple computers to operate like one, very powerful, virtual machine.

The nodes located in data centers around the globe that make up the Internet Computer are organized into subnet blockchains that in turn connect to each other using Chain Key cryptography. The distributed architecture enables secure communication without firewalls or technologies that are vulnerable to attack. Independent node operators pay data centers to host their nodes and receive remuneration for contributing computing capacity and hosting services to support dapps running on the Internet Computer blockchain.

## Subnets and Data Centers

To provide a truly decentralized blockchain that can withstand potential service disruptions, the physical nodes that make up any given blockchain subnet are distributed across data centers in diverse locations. The nodes themselves might be owned or provided by different parties in partnership or unaffiliated with the data center location where they operate.

The following diagram provides a simplified view of a subnet with nodes in four data centers.

![data center simplified](_attachments/data-center-simplified.svg)

In this simplified scenario:

-   There are four geographically-independent data centers.

-   Each data center has hardware supplied by multiple node providers.

-   Any single node provider might have equipment in multiple data centers.

Although this example represents one subnet blockchain with nodes in multiple data centers, any of the nodes could be moved out of this blockchain subnet to form a new blockchain subnet, if needed. Changes to the network topology are managed through the Internet Computer blockchain governance system called the **Network Nervous System** (NNS).

## Node Providers and Data Center Operators

In most cases, node providers—or the data center operators they partner with—are responsible for monitoring and maintaining the compute capacity of the equipment on which the Internet Computer blockchain runs. For example, node providers or data center operators might need to repair or replace equipment if there’s a hardware failure or if a system under-performs. Network operations and upgrades, however, are monitored and managed through the decentralized governance system, the Network Nervous System (NNS).

## Want to Learn More?

If you are looking for more information about data center operations and node providers, check out the following related resources:

-   [Internet Computer Help Center for Node Providers (FAQ and articles)](https://support.internetcomputer.org/hc/en-us/sections/4405489337748-Node-Provider)
