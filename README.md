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
