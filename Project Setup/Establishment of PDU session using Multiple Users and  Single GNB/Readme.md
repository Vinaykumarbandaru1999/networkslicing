# Project Network Configuration Overview
## Establishment Process
Welcome to our project's documentation. Here, we detail the essential network configuration for our UERANSIM setup, which plays a pivotal role in the functionality and testing of our system.

In our current configuration, we have established three distinct UERANSIM users (UEs), all sharing the same IP address, which is set to `192.168.64.5`. This setup is designed to simulate multiple users operating within the same network segment.

Alongside these users, we have a single gNodeB (gNB), configured with an IP address of `192.168.64.4`. This gNB acts as the primary interface for our UEs in their communication within the network.

Complementing this setup, our core network element, powered by Open5GS, is assigned an IP address of `192.168.64.3`. This core network plays a critical role in managing the network's control and data planes, ensuring seamless connectivity and communication across the network.

This configuration forms the backbone of our network setup, facilitating a robust and efficient testing environment for our 5G simulation.

## Table of content
 - [Changes in configuration files of UE1 (IMSI-999700000000005)](#changes_ue1)
 - [Changes in configuration files of UE2 (IMSI-999700000000006)](#changes_ue2)
 - [Changes in configuration files of UE3 (IMSI-999700000000007)](#changes_ue3)
 - [Changes in configuration files of GNB](#changes_gnb)
 - [Running Open5GS](#running-open5gs)
 - [To run gnb and ueransim](#to-run-gnb-and-ueransim)
 - [To Stop Open5GS](#to-stop-open5gs)
#### Changes in configuration files of UE1 (IMSI-999700000000005)

First, copy `open5gs-ue1.yaml` from `open5gs-ue.yaml`.
```
# cd UERANSIM/config
# cp open5gs-ue1.yaml open5gs-ue.yaml
```
Next, edit `open5gs-ue1.yaml`.
- `UERANSIM/config/open5gs-ue1.yaml`
```diff
--- open5gs-ue.yaml.orig     
+++ open5gs-ue1.yaml    
@@ -1,9 +1,9 @@
 # IMSI number of the UE. IMSI = [MCC|MNC|MSISDN] (In total 15 digits)
-supi: 'imsi-999700000000001'
+supi: 'imsi-999700000000005'
 # Mobile Country Code value of HPLMN
-mcc: '999'
+mcc: '999'
 # Mobile Network Code value of HPLMN (2 or 3 digits)
-mnc: '70'
+mnc: '70'
 
 # Permanent subscription key
 key: '465B5CE8B199B49FAA5F0A2EE238A6BC'
@@ -20,7 +20,7 @@
 
 # List of gNB IP addresses for Radio Link Simulation
 gnbSearchList:
-127.0.0.1
+192.168.64.5
 # UAC Access Identities Configuration
 uacAic:
 mps: false
 mcs: false
```

<a id="changes_ue1"></a>


#### Changes in configuration files of UE2 (IMSI-999700000000006)

First, copy `open5gs-ue2.yaml` from `open5gs-ue.yaml`.
```
# cd UERANSIM/config
# cp open5gs-ue2.yaml open5gs-ue.yaml
```
Next, edit `open5gs-ue2.yaml`.
- `UERANSIM/config/open5gs-ue2.yaml`
```diff
--- open5gs-ue.yaml.orig        
+++ open5gs-ue2.yaml   
@@ -1,9 +1,9 @@
 # IMSI number of the UE. IMSI = [MCC|MNC|MSISDN] (In total 15 digits)
-supi: 'imsi-999700000000001'
+supi: 'imsi-999700000000006'
 # Mobile Country Code value of HPLMN
-mcc: '999'
+mcc: '999'
 # Mobile Network Code value of HPLMN (2 or 3 digits)
-mnc: '70'
+mnc: '70'
 
 # Permanent subscription key
 key: '465B5CE8B199B49FAA5F0A2EE238A6BC'
@@ -20,7 +20,7 @@
 
 # List of gNB IP addresses for Radio Link Simulation
 gnbSearchList:
-127.0.0.1
+192.168.64.5
 # UAC Access Identities Configuration
 uacAic:
 mps: false
 mcs: false
```

<a id="changes_ue2"></a>

#### Changes in configuration files of UE3 (IMSI-999700000000007)

First, copy `open5gs-ue3.yaml` from `open5gs-ue.yaml`.
```
# cd UERANSIM/config
# cp open5gs-ue3.yaml open5gs-ue.yaml
```
Next, edit `open5gs-ue3.yaml`.
- `UERANSIM/config/open5gs-ue3.yaml`
```diff
--- open5gs-ue.yaml.orig        
+++ open5gs-ue3.yaml   
@@ -1,9 +1,9 @@
 # IMSI number of the UE. IMSI = [MCC|MNC|MSISDN] (In total 15 digits)
-supi: 'imsi-999700000000001'
+supi: 'imsi-999700000000007'
 # Mobile Country Code value of HPLMN
-mcc: '999'
+mcc: '999'
 # Mobile Network Code value of HPLMN (2 or 3 digits)
-mnc: '70'
+mnc: '70'
 
 # Permanent subscription key
 key: '465B5CE8B199B49FAA5F0A2EE238A6BC'
@@ -20,7 +20,7 @@
 
 # List of gNB IP addresses for Radio Link Simulation
 gnbSearchList:
-127.0.0.1
+192.168.64.5
 # UAC Access Identities Configuration
 uacAic:
 mps: false
 mcs: false
```

<a id="changes_ue3"></a>


### Changes in configuration files of UERANSIM UE / RAN

<a id="changes_ran"></a>

#### Changes in configuration files of RAN

- `UERANSIM/config/open5gs-gnb.yaml`
```diff
--- open5gs-gnb.yaml.orig      
+++ open5gs-gnb.yaml    
@@ -1,17 +1,17 @@
-mcc: '999'          # Mobile Country Code value
-mnc: '70'           # Mobile Network Code value (2 or 3 digits)
+mcc: '999'          # Mobile Country Code value
+mnc: '70'           # Mobile Network Code value (2 or 3 digits)
 
 nci: '0x000000010'  # NR Cell Identity (36-bit)
 idLength: 32        # NR gNB ID length in bits [22...32]
 tac: 1              # Tracking Area Code
 
-linkIp: 127.0.0.1   # gNB's local IP address for Radio Link Simulation (Usually same with local IP)
-ngapIp: 127.0.0.1   # gNB's local IP address for N2 Interface (Usually same with local IP)
-gtpIp: 127.0.0.1    # gNB's local IP address for N3 Interface (Usually same with local IP)
+linkIp: 192.168.0.4   # gNB's local IP address for Radio Link Simulation (Usually same with local IP)
+ngapIp: 192.168.0.4   # gNB's local IP address for N2 Interface (Usually same with local IP)
+gtpIp: 192.168.0.4    # gNB's local IP address for N3 Interface (Usually same with local IP)
 
 # List of AMF address information
 amfConfigs:
-  - address: 127.0.0.5
+  - address: 192.168.0.3
     port: 38412
 # List of supported S-NSSAIs by this gNB
  slices:
     sst: 1
  # Indicates whether or not SCTP stream number errors should be ignored.
    ignoreStreamIds: true
```

<a id="changes_gnb"></a>

#### Changes in configuration files of AMF

- `open5gs/install/etc/open5gs/amf.yaml`
```diff
--- amf.yaml.orig       2023-01-12 20:33:18.555295469 +0900
+++ amf.yaml    2023-01-12 21:17:46.362251130 +0900
@@ -342,26 +342,26 @@
       - addr: 127.0.0.5
         port: 7777
     ngap:
-      - addr: 127.0.0.5
+      - addr: 192.168.64.3
     metrics:
       - addr: 127.0.0.5
         port: 9090
     guami:
       - plmn_id:
+          mcc: 999
+          mnc: 70

         amf_id:
           region: 2
           set: 1
 tai:
       - plmn_id:
+          mcc: 999
+          mnc: 70
         tac: 1
     plmn_support:
       - plmn_id:
+          mcc: 999
+          mnc: 70
         s_nssai:
           - sst: 1
     security:
        integrity_order : [ NIA2, NIA1, NIA0 ]
        ciphering_order : [ NEA0, NEA1, NEA2 ]
     network_name:
       full: Open5GS
       short: Next
     amf_name: open5gs-amf0
      time:
      # t3502:
      # value: 720   # 12 minutes * 60 = 720 seconds
    t3512:
      value: 540    # 9 minutes * 60 = 540 seconds
```

- `open5gs/install/etc/open5gs/smf.yaml`
```diff
--- smf.yaml.orig       2023-01-12 20:33:18.526295426 +0900
+++ smf.yaml    2023-01-12 21:18:52.828987871 +0900
@@ -508,20 +508,21 @@
       - addr: 127.0.0.4
         port: 7777
     pfcp:
+      - addr: 127.0.0.4
+      - addr: ::1
     gtpc:
       - addr: 127.0.0.4
+     - addr: ::1
     gtpu:
+      - addr: 127.0.0.4
+      - addr: ::1
     metrics:
       - addr: 127.0.0.4
         port: 9090
     subnet:
       - addr: 10.45.0.1/16
+      - addr: 2001:db8:cafe::1/48
     dns:
       - 8.8.8.8
       - 8.8.4.4
       - 2001:4860:4860::8888
       - 2001:4860:4860::8844
  mtu: 1400
#  p-cscf:
#    - 127.0.0.1
#    - ::1
#  ctf:
#    enabled: auto   # auto(default)|yes|no
  freeDiameter: /root/open5gs/install/etc/freeDiameter/smf.conf
```

- `open5gs/install/etc/open5gs/upf.yaml`
```diff
logger:
  file: /root/open5gs/install/var/log/open5gs/upf.log
#  level: info   # fatal|error|warn|info(default)|debug|trace

global:
  max:
    ue: 1024  # The number of UE can be increased depending on memory size.
#    peer: 64

upf:
  pfcp:
    server:
+      - address: 127.0.0.7
    client:
#      smf:     #  UPF PFCP Client try to associate SMF PFCP Server
+ #        - address: 127.0.0.4
  gtpu:
    server:
+      - address: 127.0.0.7
  session:
+    - subnet: 10.45.0.1/16
+    - subnet: 2001:db8:cafe::1/48
  metrics:
    server:
+      - address: 127.0.0.7
+        port: 9090

```
## Running Open5GS
```diff
./install/bin/open5gs-nrfd & ./install/bin/open5gs-scpd & ./install/bin/open5gs-amfd & ./install/bin/open5gs-smfd &./install/bin/open5gs-upfd & ./install/bin/open5gs-ausfd & ./install/bin/open5gs-udmd & ./install/bin/open5gs-pcfd & ./install/bin/open5gs-nssfd & ./install/bin/open5gs-bsfd & ./install/bin/open5gs-udrd & ./install/bin/open5gs-mmed & ./install/bin/open5gs-sgwcd & ./install/bin/open5gs-sgwud & ./install/bin/open5gs-hssd & ./install/bin/open5gs-pcrfd

```
## To run gnb and ueransim

```diff
+ sudo build/nr-gnb -c config/open5gs-gnb.yaml
+ sudo build/nr-ue -c config/open5gs-ue.yaml
```
## To Stop Open5GS
- To stop all Open5GS network functions(NF's)
```diff
+ pkill -f './install/bin/open5gs-'
```
