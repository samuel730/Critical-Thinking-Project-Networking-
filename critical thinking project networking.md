CRITICAL THINKING: Subnetting Plan for a Growing Organization

Introduction

As a network administrator, it is important to design a network that efficiently uses IP addresses while providing logical separation between departments. This subnetting plan is designed for an organization with six departments and a centralized data center. The design ensures that each department has its own subnet, supports future growth, and allows for efficient network management and troubleshooting.

⸻

1. Identify Subnet Requirements

The organization currently consists of six departments:

* Finance
* Human Resources
* Sales
* Marketing
* IT
* Operations

Each department occupies its own floor within the office building, requiring logical separation through subnetting and VLAN segmentation.

To support future expansion, the network must accommodate at least 50% growth in each department over the next five years.

Host Requirements with Future Growth

Department	Current Hosts	50% Growth	Total Hosts Required
Finance	50	25	75
Human Resources	30	15	45
Sales	70	35	105
Marketing	40	20	60
IT	100	50	150
Operations	80	40	120

Therefore, a minimum of six subnets are required, with additional address space reserved for future departments.

⸻

2. IP Address Allocation Strategy

The private network block selected for this design is:

Network Address: 192.168.0.0/22

A /22 network provides:

* Total Addresses: 1024
* Usable Host Addresses: 1022

This address space is sufficient for current requirements and future expansion.

Variable Length Subnet Masking (VLSM) is used to allocate address space efficiently according to the size of each department.

⸻

3. Subnet Calculations and Mask Selection

Subnet masks are selected based on the number of hosts required after accounting for future growth.

IT Department

Required Hosts = 150

Formula:

2^n - 2 ≥ 150

2^8 - 2 = 254

Subnet Size: 256 addresses

Subnet Mask: /24 (255.255.255.0)

⸻

Operations Department

Required Hosts = 120

2^7 - 2 = 126

Subnet Size: 128 addresses

Subnet Mask: /25 (255.255.255.128)

⸻

Sales Department

Required Hosts = 105

2^7 - 2 = 126

Subnet Size: 128 addresses

Subnet Mask: /25 (255.255.255.128)

⸻

Finance Department

Required Hosts = 75

2^7 - 2 = 126

Subnet Size: 128 addresses

Subnet Mask: /25 (255.255.255.128)

⸻

Marketing Department

Required Hosts = 60

2^6 - 2 = 62

Subnet Size: 64 addresses

Subnet Mask: /26 (255.255.255.192)

⸻

Human Resources Department

Required Hosts = 45

2^6 - 2 = 62

Subnet Size: 64 addresses

Subnet Mask: /26 (255.255.255.192)

⸻

4. Subnet Allocation and Documentation

Department	Network Address	Subnet Mask	First Usable IP	Last Usable IP	Broadcast Address
IT	192.168.0.0/24	255.255.255.0	192.168.0.1	192.168.0.254	192.168.0.255
Operations	192.168.1.0/25	255.255.255.128	192.168.1.1	192.168.1.126	192.168.1.127
Sales	192.168.1.128/25	255.255.255.128	192.168.1.129	192.168.1.254	192.168.1.255
Finance	192.168.2.0/25	255.255.255.128	192.168.2.1	192.168.2.126	192.168.2.127
Marketing	192.168.2.128/26	255.255.255.192	192.168.2.129	192.168.2.190	192.168.2.191
Human Resources	192.168.2.192/26	255.255.255.192	192.168.2.193	192.168.2.254	192.168.2.255

Purpose of Each Subnet

Finance

Used for financial transactions, accounting software, payroll processing, and financial reporting systems.

Human Resources

Supports employee records, payroll systems, recruitment platforms, and personnel management applications.

Sales

Supports customer relationship management (CRM) systems, sales databases, and customer communication tools.

Marketing

Supports digital marketing platforms, campaign analytics, social media management tools, and market research applications.

IT

Hosts network infrastructure services, servers, monitoring systems, directory services, and administrative tools.

Operations

Supports production systems, inventory management, logistics applications, and supply chain management.

⸻

5. Troubleshooting Scenarios

Connectivity Issues

If users in one department cannot communicate with another subnet:

1. Check routing tables on routers and Layer 3 switches to verify that routes to all departmental subnets exist.
2. Verify VLAN assignments and ensure devices are connected to the correct VLAN.
3. Examine firewall rules to ensure inter-subnet communication is permitted where required.
4. Use ping and traceroute commands to identify where communication is failing.

Resolution

* Correct missing routes.
* Reconfigure VLAN assignments if necessary.
* Update firewall policies to allow approved traffic.

⸻

IP Address Conflicts

An IP conflict occurs when two devices use the same IP address.

Detection

1. Review DHCP server logs.
2. Check network monitoring tools for duplicate IP warnings.
3. Use ARP tables to identify conflicting devices.

Resolution

* Release and renew DHCP leases.
* Remove duplicate static assignments.
* Reserve addresses for critical systems.

⸻

Overlapping Subnets

Overlapping occurs when two subnets share the same address range.

Detection

1. Review network documentation.
2. Verify subnet boundaries using subnet calculations.
3. Check router configurations for duplicate networks.

Resolution

* Assign unique address ranges.
* Recalculate subnet masks.
* Update routing configurations accordingly.

⸻

6. Future Growth Strategy

The network has been designed to support organizational growth.

Expanding Existing Departments

As departments increase in size:

* Marketing can be expanded from /26 to /25.
* Human Resources can be expanded from /26 to /25.
* Sales, Finance, and Operations can be expanded from /25 to /24 if required.

Adding New Departments

Unused address space within the 192.168.0.0/22 network can be allocated to:

* Research and Development
* Customer Support
* Security Operations
* Additional branch offices

Documentation Updates

Whenever modifications occur:

1. Update subnet allocation records.
2. Document new VLAN IDs.
3. Record routing changes.
4. Maintain version-controlled documentation in GitHub.

⸻

7. Network Optimization

Efficient Routing

To optimize traffic flow:

* Deploy Layer 3 switches.
* Implement OSPF routing protocol for dynamic route management.
* Reduce unnecessary broadcast traffic through subnet segmentation.

Benefits:

* Faster routing decisions.
* Improved scalability.
* Better network performance.

⸻

VLAN Implementation

Each department should be assigned a dedicated VLAN.

Example:

VLAN ID	Department
10	Finance
20	Human Resources
30	Sales
40	Marketing
50	IT
60	Operations

Benefits:

* Improved security.
* Reduced broadcast domains.
* Easier network management.

⸻

DHCP and Static Addressing

DHCP should be used for:

* User workstations
* Laptops
* Mobile devices

Static IP addresses should be reserved for:

* Servers
* Printers
* Network switches
* Routers
* Firewalls

Benefits:

* Simplified administration.
* Reduced IP conflicts.
* Consistent access to critical infrastructure.

⸻

Conclusion

This subnetting plan provides efficient IP address allocation, logical separation of departments, improved security, and support for future organizational growth. Through the use of VLSM, VLAN segmentation, DHCP services, and efficient routing protocols, the network can scale effectively while maintaining performance and manageability.