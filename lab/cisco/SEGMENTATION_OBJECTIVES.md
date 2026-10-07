# Cisco Segmentation Objectives

The Cisco component is intentionally configuration-neutral so it can be implemented on IOSv, CML, Packet Tracer-compatible devices, or equivalent virtual networking.

Analyst objectives:
1. Identify traffic expected between USERS, SERVERS, SOC, and VAULT.
2. Verify that USERS cannot initiate ordinary sessions to VAULT.
3. Permit only the minimum controlled recovery-copy path required by the lab design.
4. Collect routing/ACL/network telemetry for correlation with Windows logs.
5. Demonstrate that compromise of the user/server zones does not automatically provide a path into the recovery vault.

Do not connect the lab VLANs to production networks.
