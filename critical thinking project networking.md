# Subnetting Plan for a Growing Organization

## 1. Introduction

This document presents a subnetting design for an organization with six departments. The goal is to efficiently allocate IP addresses, ensure logical separation, and allow for future growth of at least 50%.

The organization uses a centralized data center and departmental floor-based network segmentation.

---

## 2. Subnet Requirements Analysis

### Departments and Host Needs (including 50% growth)

| Department      | Current Hosts | +50% Growth | Total Required Hosts |
| --------------- | ------------- | ----------- | -------------------- |
| Finance         | 50            | 25          | 75                   |
| Human Resources | 30            | 15          | 45                   |
| Sales           | 70            | 35          | 105                  |
| Marketing       | 40            | 20          | 60                   |
| IT              | 100           | 50          | 150                  |
| Operations      | 80            | 40          | 120                  |

---

## 3. Chosen IP Address Block

We will use a private Class C network expanded using subnetting.

**Network Address:** `192.168.0.0/22`  
This provides 1024 IP addresses (1022 usable), enough for all departments and growth.

---

## 4. Subnet Allocation (VLSM Design)

We use Variable Length Subnet Masking (VLSM) to efficiently allocate IPs.

### Subnet Plan

| Department      | Subnet Network   | Subnet Mask     | Usable Hosts | IP Range |
| --------------- | ---------------- | --------------- | ------------ | -------- |
| IT              | 192.168.0.0/24   | 255.255.255.0   | 254          | 192.168.0.1 – 192.168.0.254 |
| Operations      | 192.168.1.0/25   | 255.255.255.128 | 126          | 192.168.1.1 – 192.168.1.126 |
| Sales           | 192.168.1.128/25 | 255.255.255.128 | 126          | 192.168.1.129 – 192.168.1.254 |
| Finance         | 192.168.2.0/25   | 255.255.255.128 | 126          | 192.168.2.1 – 192.168.2.126 |
| Marketing       | 192.168.2.128/26 | 255.255.255.192 | 62           | 192.168.2.129 – 192.168.2.190 |
| Human Resources | 192.168.2.192/26 | 255.255.255.192 | 62           | 192.168.2.193 – 192.168.2.254 |

---

## 5. Subnet Masking Explanation

- `/24` → 256 IPs (254 usable)
- `/25` → 128 IPs (126 usable)
- `/26` → 64 IPs (62 usable)

### Why VLSM?

- No IP wastage  
- Efficient address utilization  
- Flexible scaling for future growth  

---

## 6. Network Purpose Documentation

| Department | Purpose |
|------------|--------|
| Finance | Accounting systems, payroll, financial transactions |
| Human Resources | Employee records, recruitment, payroll |
| Sales | CRM systems, customer data |
| Marketing | Campaign tracking, analytics |
| IT | Servers, network infrastructure, monitoring |
| Operations | Supply chain and production systems |

---

## 7. Troubleshooting Scenarios

### Connectivity Issues
- Check routing tables for correct subnet routes
- Verify VLAN configuration per department
- Inspect firewall rules for inter-subnet traffic

### IP Conflicts
- Review DHCP server logs
- Identify duplicate IP assignments
- Assign static IPs for critical systems

### Overlapping Subnets
- Ensure each subnet has a unique range
- Validate subnet masks before deployment
- Use VLSM planning tools to prevent overlap

---

## 8. Future Growth Strategy

- Expand `/26 → /25` or `/25 → /24` when departments grow
- Add new subnets for new departments
- Maintain updated documentation in GitHub

---

## 9. Optimization Techniques

- Implement VLANs for departmental segmentation
- Use inter-VLAN routing (Layer 3 switch/router)
- Use DHCP for dynamic IP allocation
- Assign static IPs to critical servers and devices

---

## 10. Conclusion

This subnetting plan ensures efficient IP utilization, strong departmental separation, and scalability for future growth using VLSM and structured network design.
