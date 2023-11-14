# OSPF-troubleshooting-lab-scenario
To build a network and configure OSPF to find the optimal path between routers, ensuring efficient communication within the network.



Install Cisco network packet tracer 8.2.1 from https://www.netacad.com/courses/packet-tracer and follow the below steps by using commands provided in the .project file.

OVERALL WORK FLOW:
Step-1: Assign IP Addresses and Bring Interfaces Up
Step-2: Enable OSPF Routing
Step-3: Perform ping tests
Step-4: View OSPF Database on R2
Step-5: Enable OSPF for Network 192.168.1.0 on R2
Step-6: Re-Ping R1 from R4

PROBLEM DEFINITION:

To build a network (topology as given in this link: https://routersimulator.certexams.com/router-labs/ospf-troubleshooting-lab-scenario-1.html ) and configure OSPF to find the optimal path between routers, ensuring efficient communication within the network.  After setting up OSPF, you need to analyze its performance. This involves assessing factors such as routing efficiency, convergence time, load balancing, and overall network traffic.

PROTOCOL/METHOD EXPLANATION:

The OSPF (Open Shortest Path First) is a widely used routing protocol within a single autonomous system. It operates based on a link-state routing algorithm, where each router contains information about every domain. OSPF’s goal is to learn routes by exchanging LSAs (Link State Advertisements), which include details about routers, subnets, and other network information. The collected data is stored in a link-state database (LSDB). OSPF divides networks into areas, and routers within an area share routing information. Area Border Routers summarize information between areas, and backbone routers connect different areas within the autonomous system.

WORKING OF OSPF:

Step 1: The first step is to become OSPF neighbors. The two connecting routers running OSPF on the same link creates a neighbor relationship.
Step 2: The second step is to exchange database information. After becoming the neighbors, the two routers exchange the LSDB information with each other.
Step 3: The third step is to choose the best route. Once the LSDB information has been exchanged with each other, the router chooses the best route to be added to a routing table based on the calculation of SPF.

IMPLEMENTATION PROCEDURE:

 Let's configure the IP addresses and OSPF routing for the given network topology in Packet Tracer 8.2.1. using the necessary commands as given below:

Assign IP Addresses and Bring Interfaces Up:
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


Ping Tests:
Now let’s perform the ping tests:
Ping R1 from R4: You will see ping failure.
Ping R2 from R4: You will see ping success (indicating connectivity failure from R2 to R1).

[To ping R1 from R4, follow these steps:
Access the CLI (Command Line Interface) of R4.
Use the following command to ping R1 (IP address 192.168.1.1):
R4# ping 192.168.1.1


This command will send ICMP echo requests to R1, and you should see the ping results indicating whether the communication is successful or not.

To ping R2 from R4, follow these steps:
Access the CLI (Command Line Interface) of R4.
Use the following command to ping R2 (IP address 192.168.1.2):
R4# ping 192.168.1.2


This command will send ICMP echo requests to R2, and you should see the ping results indicating whether the communication is successful or not.

]
View OSPF Database on R2:
To view the OSPF database on R2, issue the following command:
R2# show ip ospf database


Enable OSPF for Network 192.168.1.0 on R2:
Since there is no link state entry for network 192.168.1.0, enable OSPF routing for this network on R2:
R2(config)# router ospf 1
R2(config-router)# network 192.168.1.0 0.0.0.255 area 200


Re-Ping R1 from R4:
After enabling OSPF for network 192.168.1.0, ping R1 from R4 again. You should now see ping success.



I apologize for the oversight in my previous response. Let’s troubleshoot the issue. Since you encountered a ping failure from R4 to R2, we need to investigate further.
Please follow these steps:
Check Interface Status:
Ensure that the interfaces on R2 are up and operational. Use the following command on R2:
R2# show ip interface brief


Verify that the interfaces s0/0, s0/1, and s1/0 are in the “up” state.
Verify OSPF Configuration:
Double-check the OSPF configuration on R2. Make sure the network statements are correctly configured for the interfaces:
R2(config)# router ospf 1
R2(config-router)# network 192.168.2.0 0.0.0.255 area 200
R2(config-router)# network 192.168.3.0 0.0.0.255 area 200


Confirm that the OSPF process ID (1) and area (200) match the other routers.
Check Routing Table:
Verify that R2 has learned routes from R1 and R3. Use the following command on R2:
R2# show ip route


Look for entries corresponding to networks 192.168.1.0, 192.168.2.0, and 192.168.3.0.
Verify Connectivity:
From R2, try pinging R1 (192.168.1.1) directly:
R2# ping 192.168.1.1


If this fails, it indicates an issue with the link between R1 and R2.
Check Physical Connections:
Ensure that the physical connections (cables) between R1, R2, and R4 are properly connected.
Debugging:
If the issue persists, consider enabling OSPF debugging on R2:
R2# debug ip ospf events
R2# debug ip ospf adj


Observe the debug output to identify any OSPF-related issues.
Re-Ping R2 from R4:
After verifying the above steps, re-ping R2 from R4:
R4# ping 192.168.1.2
