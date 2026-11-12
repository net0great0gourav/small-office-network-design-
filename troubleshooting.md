
# Troubleshooting Guide

## 1. PC is not receiving an IP address

**Possible causes:**
- DHCP pool is not configured correctly.
- Router subinterface is down.
- VLAN assignment is incorrect.
- Trunk is not carrying the required VLAN.

**Verification commands:**
- show ip dhcp binding
- show ip dhcp pool
- show ip interface brief
- show interfaces trunk

## 2. PCs in different VLANs cannot communicate

**Possible causes:**
- Incorrect IP address or subnet mask.
- Incorrect default gateway.
- Router subinterface configuration issue.
- Trunk configuration issue.

**Verification commands:**
- show vlan brief
- show interfaces trunk
- show ip interface brief
- ping [destination IP]

## 3. VLAN is missing from the switch

**Verification command:**
- show vlan brief

**Possible solution:**
Create the missing VLAN and assign the correct access port.

## 4. Trunk is not working

**Verification command:**
- show interfaces trunk

**Possible solution:**
Check trunk mode, allowed VLANs, and physical connectivity.
