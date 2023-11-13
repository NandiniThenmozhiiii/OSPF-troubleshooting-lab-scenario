# OSPF-troubleshooting-lab-scenario
To build a network and configure OSPF to find the optimal path between routers, ensuring efficient communication within the network.

CODE:

On each router, configure the IP addresses and enable the interfaces using the following commands:
R1:
R1(config)# interface s0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
R2:
R2(config)# interface s0/0
R2(config-if)# ip address 192.168.1.2 255.255.255.0
R2(config-if)# no shutdown


R2(config)# interface s0/1
R2(config-if)# ip address 192.168.2.1 255.255.255.0
R2(config-if)# no shutdown


R2(config)# interface s1/0
R2(config-if)# ip address 192.168.3.1 255.255.255.0
R2(config-if)# no shutdown
R3:
R3(config)# interface s0/0
R3(config-if)# ip address 192.168.2.2 255.255.255.0
R3(config-if)# no shutdown
R4:
R4(config)# interface s0/0
R4(config-if)# ip address 192.168.3.2 255.255.255.0
R4(config-if)# no shutdown
Enable OSPF Routing:
Configure OSPF on each router with process ID 1 and area 200 for the specified networks:
R1:
R1(config)# router ospf 1
R1(config-router)# network 192.168.1.0 0.0.0.255 area 200
R2:
R2(config)# router ospf 1
R2(config-router)# network 192.168.2.0 0.0.0.255 area 200
R2(config-router)# network 192.168.3.0 0.0.0.255 area 200
R3:
R3(config)# router ospf 1
R3(config-router)# network 192.168.2.0 0.0.0.255 area 200
R4:
R4(config)# router ospf 1
R4(config-router)# network 192.168.3.0 0.0.0.255 area 200
