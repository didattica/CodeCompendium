
# 17.7.6 Packet Tracer - Risoluzione dei problemi di connettività
L'obiettivo di questa attività Packet Tracer è la risoluzione dei problemi di connettività, se possibile. In caso contrario, i problemi devono essere documentati chiaramente in modo da poter effettuare la riassegnazione.


Ecco il contenuto del file PDF convertito in formato Markdown, con la struttura di titoli e sottotitoli riprodotta fedelmente secondo il documento originale:

---

# Packet Tracer - Troubleshoot Connectivity Issues

## Addressing Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
| --- | --- | --- | --- | --- |
| **R1** | G0/0 | 172.16.1.1 | 255.255.255.0 | N/A |
|  | G0/1 | 172.16.2.1 | 255.255.255.0 | N/A |
|  | S0/0/0 | 209.165.200.226 | 255.255.255.252 | N/A |
| **R2** | G0/0 | 209.165.201.1 | 255.255.255.224 | N/A |
|  | S0/0/0 (DCE) | 209.165.200.225 | 255.255.255.252 | N/A |
| **PC-01** | NIC | 172.16.1.3 | 255.255.255.0 | 172.16.1.1 |
| **PC-02** | NIC | 172.16.1.4 | 255.255.255.0 | 172.16.1.1 |
| **PC-A** | NIC | 172.16.2.3 | 255.255.255.0 | 172.16.2.1 |
| **PC-B** | NIC | 172.16.2.4 | 255.255.255.0 | 172.16.2.1 |
| **Web** | NIC | 209.165.201.2 | 255.255.255.224 | 209.165.201.1 |
| **DNS1** | NIC | 209.165.201.3 | 255.255.255.224 | 209.165.201.1 |
| **DNS2** | NIC | 209.165.201.4 | 255.255.255.224 | 209.165.201.1 |

## Objectives

In this Packet Tracer activity, you will troubleshoot and resolve connectivity issues, if possible. Otherwise, the issues should be clearly documented so they can be escalated.

## Background / Scenario

Users are reporting that they cannot access the web server, **www.cisco.pka** after a recent upgrade that included adding a second DNS server. You must determine the cause and attempt to resolve the issues for the users. Clearly document the issues and any solution(s). You do not have access to the devices in the cloud or the server **www.cisco.pka**. Escalate the problem if necessary.

**Note:** Router R1 can only be accessed using SSH with the username **Admin01** and password **cisco12345**. Router R2 is in the ISP cloud and is not accessible by you.

## Instructions

### Part 1: Determine connectivity issues from PC-01.

a. On PC-01, open the command prompt. Enter the command `ipconfig` to verify what IP address and default gateway have been assigned to PC-01. Correct as necessary according to the Addressing Table.

b. After verifying/correcting the IP addressing issues on PC-01, issue pings to the default gateway, web server, and other PCs. Were the pings successful? Record the results.

* Ping to default gateway (172.16.1.1)?
* To web server (209.165.201.2)?
* Ping to PC-02?
* To PC-A?
* To PC-B?

c. Use the web browser to access the web server on PC-01. Access the web server by first entering the URL **[http://www.cisco.pka](https://www.google.com/search?q=http://www.cisco.pka)** and then by using the IP address **209.165.201.2**. Record the results.

* Can PC-01 access www.cisco.pka?
* Using the web server IP address?

d. Document the issues and provide the solution(s). Correct the issues if possible.

---

### Part 2: Determine connectivity issues from PC-02.

a. On PC-02, open the command prompt. Enter the command `ipconfig` to verify the configuration for the IP address and default gateway. Correct as necessary.

b. After verifying/correcting the IP addressing issues on PC-02, issue pings to the default gateway, web server, and other PCs. Were the pings successful? Record the results.

* Ping to default gateway (172.16.1.1)?
* To web server (209.165.201.2)?
* Ping to PC-01?
* To PC-A?
* To PC-B?

c. Navigate to **www.cisco.pka** using the web browser on PC-02. Record the results.

* Can PC-02 access www.cisco.pka?
* Using the web server IP address?

d. Document the issues and provide the solution(s). Correct the issues if possible.

---

### Part 3: Determine connectivity issues from PC-A.

a. On PC-A, open the command prompt. Enter the command `ipconfig` to verify the configuration for the IP address and default gateway. Correct as necessary.

b. After correcting the IP addressing issues on PC-A, issue the pings to the web server, default gateway, and other PCs. Were the pings successful? Record the results.

* To web server (209.165.201.2)?
* Ping to default gateway (172.16.2.1)?
* Ping to PC-B?
* To PC-01?
* To PC-02?

c. Navigate to **www.cisco.pka** using the web browser on PC-A. Record the results.

* Can PC-A access www.cisco.pka?
* Using the web server IP address?

d. Document the issues and provide the solution(s). Correct the issues if possible.

---

### Part 4: Determine connectivity issues from PC-B.

a. On PC-B, open the command prompt. Enter the command `ipconfig` to verify the configuration for the IP address and default gateway. Correct as necessary.

b. After correcting the IP addressing issues on PC-B, issue the pings to the web server, default gateway, and other PCs. Were the pings successful? Record the results.

* To web server (209.165.201.2)?
* Ping to default gateway (172.16.2.1)?
* Ping to PC-A?
* To PC-01?
* To PC-02?

c. Navigate to **www.cisco.pka** using the web browser. Record the results.

* Can PC-B access www.cisco.pka?
* Using the web server IP address?

d. Document the issues and provide the solution(s). Correct the issues if possible.

e. Could all the issues be resolved on PC-B and still make use of DNS2? If not, what would you need to do?

---

### Part 5: Verify connectivity.

Verify that all the PCs can access the web server **www.cisco.pka**. Your completion percentage should be 100%. If not, verify that the IP configuration information is correct on all devices and that it matches what is shown in the addressing table.
