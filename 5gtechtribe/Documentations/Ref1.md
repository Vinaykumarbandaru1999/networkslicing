




<img src="resources/images/FRA-UAS_Logo_rgb.jpg" width="150"/>



## Table of Contents

*    [Open5GS 5GC Simulation Mobile Network Overview](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Documentions/Project_Documentation/User%20guide/Open5GS%205GC%20Simulation%20Mobile%20Network%20Overview.md)

     - [Control Plane and User Plane Network Architecture](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Documentions/Project_Documentation/User%20guide/Open5GS%205GC%20Simulation%20Mobile%20Network%20Overview.md#control-plane-and-user-plane-network-architecture)
     - [Open5GS 4G/5G NSA Core Components](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Documentions/Project_Documentation/User%20guide/Open5GS%205GC%20Simulation%20Mobile%20Network%20Overview.md#open5gs-4g5g-nsa-core-components)
     - [Open5GS 5G SA Core Components](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Documentions/Project_Documentation/User%20guide/Open5GS%205GC%20Simulation%20Mobile%20Network%20Overview.md#open5gs-5g-sa-core-components)
     - [Running Open5GS 5GC Control Plane (C-Plane)](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Documentions/Project_Documentation/User%20guide/Open5GS%205GC%20Simulation%20Mobile%20Network%20Overview.md#running-open5gs-5gc-control-plane-c-plane)
     - [Running Open5GS 5GC User Plane (U-Plane)](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Documentions/Project_Documentation/User%20guide/Open5GS%205GC%20Simulation%20Mobile%20Network%20Overview.md#running-open5gs-5gc-control-plane-c-plane)


![image](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/assets/116576484/4b47bd58-d58c-4fff-9fa5-74ea22cba441)





# Open5GS and UERANSIM Configuration

- [5GC - Open5GS](https://github.com/open5gs/open5gs)
- [UE / RAN - UERANSIM ](https://github.com/aligungr/UERANSIM)

## Virtual Machines Setup

| VM # | Role             | IP Address       | OS        | Memory | HDD  |
|------|------------------|------------------|-----------|--------|------|
| VM1 - Control Plane  | Open5GS 5GC C-Plane | 192.168.64.03/24 | Ubuntu 20.04 | 1GB   | 20GB |
| VM2 - gNodeB | Open5GS 5GC U-Plane1| 192.168.64.04/24 | Ubuntu 20.04 | 1GB   | 20GB |
| VM3 - UE  | Open5GS 5GC U-Plane1| 192.168.64.05/24 | Ubuntu 20.04 | 1GB   | 20GB |

## Subscriber Information

Please configure the OP or OPC values according to the UERANSIM UE configuration files.

| UE # | IMSI            | DNN      | OP/OPc |
|------|-----------------|----------|--------|
| UE1  | - | internet | OPc    |
| UE2  | - | ims | OPc    |
| UE3  | - | sms | OPc    |




### Changes in Static IP address according to two smfs; Configure the mybridge Interface
Modified the configuration for the mybridge network interface. The changes made were as follows:
 
- Specified mybridge to use the network interface `enp0s1`.
- Disabled DHCP (`dhcp4: no`) to enable static IP configuration.
- Set the static IP address to `192.168.64.3`,`192.168.64.11`,192.168.64.12` with a subnet mask of `24` (equivalent to `255.255.255.0`).
- Defined a default route (`0.0.0.0/0`) with a gateway of `192.168.64.1.`
- Specified DNS servers with the IP addresses `8.8.8.8` and `8.8.4.4`.
- Here we have created a global Ip addresses for the SMF1 and SMF2 with ip addresses as 192.168.64.111 and 192.168.64.112.
The resulting configuration block for mybridge looked like this:
 ```csharp
# /etc/netplan/01-netcfg.yaml

network:
  version: 2
  renderer: networkd
  bridges:
    mybridge:
      interfaces: [enp0s1]
      dhcp4: no
      addresses: [192.168.64.3/24,192.168.64.11/24,192.168.64.12/24]
      routes:
        - to: 0.0.0.0/0
          via: 192.168.64.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]

```


### Changes in configuration files of Open5GS 5GC and UERANSIM UE / RAN

#### Changes in configuration files of UPF1

```diff
logger:
  file: /root/open5gs/install/var/log/open5gs/upf.log
#  level: info   # fatal|error|warn|info(default)|debug|trace

global:
  max:
    ue: 1024  # The number of UE can be increased depending on memory size.
#   peer: 64

upf:
  pfcp:
    server:
      - address: 192.168.64.4
#    client:
 #    smf:     #  UPF PFCP Client try to associate SMF PFCP Server
  #      - address: 127.0.0.24
  gtpu:
    server:
      - address: 192.168.64.4
  # session:
  #   - subnet: 10.45.0.1/16
   #   dnn: video-streaming
  session:
    - subnet: 10.45.0.1/16
      dnn: internet
      dev: ogstun
    - subnet: 10.47.0.1/16
      dnn: voip
      dev: ogstun
  metrics:
    server:
      - address: 127.0.0.7
        port: 9090

```

#### Changes in configuration files of UPF2

```diff
logger:
  file: /root/open5gs/install/var/log/open5gs/upf.log
#  level: info   # fatal|error|warn|info(default)|debug|trace

global:
  max:
    ue: 1024  # The number of UE can be increased depending on memory size.
#   peer: 64

upf:
  pfcp:
    server:
      - address: 192.168.64.6
#    client:
 #    smf:     #  UPF PFCP Client try to associate SMF PFCP Server
  #      - address: 127.0.0.24
  gtpu:
    server:
      - address: 192.168.64.6
  # session:
  #   - subnet: 10.45.0.1/16
   #   dnn: video-streaming
  session:
    - subnet: 10.46.0.1/16
      dnn: internet2
      dev: ogstun
    - subnet: 10.48.0.1/16
      dnn: voip2
      dev: ogstun
  metrics:
    server:
      - address: 127.0.0.7
        port: 9090

```

#### Changes in configuration files of AMF

- `open5gs/install/etc/open5gs/amf.yaml`
```diff
--- amf.yaml.orig       2023-01-12 20:33:18.555295469 +0900
+++ amf.yaml    2023-01-12 21:17:46.362251130 +0900
@@ -342,26 +342,26 @@
logger:
  file: /root/open5gs/install/var/log/open5gs/amf.log
#  level: info   # fatal|error|warn|info(default)|debug|trace

global:
  max:
    ue: 1024  # The number of UE can be increased depending on memory size.
- #    peer: 64

amf:
  sbi:
    server:
      - address: 127.0.0.5
        port: 7777
    client:
- #      nrf:
- #        - uri: http://127.0.0.10:7777
      scp:
        - uri: http://127.0.0.200:7777
  ngap:
    server:
+      - address: 192.168.64.3
  metrics:
    server:
      - address: 127.0.0.5
        port: 9090
  guami:
    - plmn_id:
+        mcc: 999
+        mnc: 70
      amf_id:
        region: 2
        set: 1
  tai:
    - plmn_id:
 +       mcc: 999
 +       mnc: 70
      tac: 1
  plmn_support:
+    - plmn_id:
+        mcc: 999
+        mnc: 70
+      s_nssai:
+        - sst: 1
+          sd: 000001
+        - sst: 1
+          sd: 000002
+        - sst: 1
+          sd: 000003
+        - sst: 1
+          sd: 000004
  security:
    integrity_order : [ NIA2, NIA1, NIA0 ]
    ciphering_order : [ NEA0, NEA1, NEA2 ]
  network_name:
    full: Open5GS
    short: Next
  amf_name: open5gs-amf0
  time:
#    t3502:
#      value: 720   # 12 minutes * 60 = 720 seconds
    t3512:
      value: 540    # 9 minutes * 60 = 540 seconds
```

#### Changes in configuration files of SMF1


- `open5gs/install/etc/open5gs/smf1.yaml`
```diff
logger:
  file: /root/open5gs/install/var/log/open5gs/smf1.log
- #  level: info   # fatal|error|warn|info(default)|debug|trace

global:
  max:
    ue: 1024  # The number of UE can be increased depending on memory size.
- #    peer: 64

smf:
  sbi:
    server:
      - address: 127.0.0.4
        port: 7777
    client:
- #      nrf:
- #        - uri: http://127.0.0.10:7777
      scp:
        - uri: http://127.0.0.200:7777
  pfcp:
    server:
+      - address: 192.168.64.11
+        dnn: internet
+        dnn: voip
    client:
      upf:
+       - address: 192.168.64.4
  gtpc:
    server:
      - address: 127.0.0.4
  gtpu:
    server:
+      - address: 192.168.64.11
  metrics:
    server:
      - address: 127.0.0.4
        port: 9090
  session:
+    - subnet: 10.45.0.1/16
+    - dnn: internet
+    - subnet: 10.47.0.1/16
+    - dnn: voip

  dns:
    - 8.8.8.8
    - 8.8.4.4
    - 2001:4860:4860::8888
    - 2001:4860:4860::8844
  mtu: 1400
- #  p-cscf:
- #    - 127.0.0.1
- #    - ::1
- #  ctf:
- #    enabled: auto   # auto(default)|yes|no
  freeDiameter: /root/open5gs/install/etc/freeDiameter/smf1.conf
  info:
+    - s_nssai:
+        - sst: 1
+         sd: 000001
+          dnn:
+            - internet
+        - sst: 1
+         sd: 000003
+            - voip
+      tai:
+        - plmn_id:
+            mcc: 999
+            mnc: 70
+          tac: 1
  pfcp:
    client:
      upf:
+        - address: 192.168.64.4
          dnn: internet
          dnn: voip
```

#### Changes in configuration files of SMF2
```diff
logger:
  file: /root/open5gs/install/var/log/open5gs/smf2.log
- #  level: info   # fatal|error|warn|info(default)|debug|trace

global:
  max:
    ue: 1024  # The number of UE can be increased depending on memory size.
- #    peer: 64

smf:
  sbi:
    server:
      - address: 127.0.0.24
        port: 7777
    client:
- #      nrf:
- #        - uri: http://127.0.0.10:7777
      scp:
        - uri: http://127.0.0.200:7777
  pfcp:
    server:
+      - address: 192.168.64.12
+        dnn: internet2
    client:
      upf:
+        - address: 192.168.64.6
  gtpc:
    server:
      - address: 127.0.0.24
  gtpu:
    server:
+      - address: 192.168.64.12
  metrics:
    server:
+      - address: 127.0.0.24
        port: 9090
  session:
+    - subnet: 10.46.0.1/16
+    - dnn: internet2
+    - subnet: 10.48.0.1/16
+    - dnn: voip2

  dns:
    - 8.8.8.8
    - 8.8.4.4
    - 2001:4860:4860::8888
    - 2001:4860:4860::8844
  mtu: 1400
- #  p-cscf:
- #    - 127.0.0.1
- #    - ::1
- #  ctf:
- #    enabled: auto   # auto(default)|yes|no
  freeDiameter: /root/open5gs/install/etc/freeDiameter/smf2.conf
  info:
+    - s_nssai:
+        - sst: 1
+          sd: 000003
+          dnn: internet2
+        - sst: 1
+          sd: 000004
+          dnn:
+            - voip2
+      tai:
+        - plmn_id:
+            mcc: 999
+            mnc: 70
+          tac: 1
  pfcp:
    client:
      upf:
+        - address: 192.168.64.6
+          dnn: internet2
+          dnn: voip2
```



#### Changes in configuration files of GNB
```diff
+ mcc: '999'          # Mobile Country Code value
+ mnc: '70'           # Mobile Network Code value (2 or 3 digits)

nci: '0x000000010'  # NR Cell Identity (36-bit)
idLength: 32        # NR gNB ID length in bits [22...32]
+ tac: 1              # Tracking Area Code

+ linkIp: 192.168.64.5 #127.0.0.1   # gNB's local IP address for Radio Link Simulation (Usually same with local IP)
+ ngapIp: 192.168.64.5 #127.0.0.1   # gNB's local IP address for N2 Interface (Usually same with local IP)
+ gtpIp: 192.168.64.5 #127.0.0.1    # gNB's local IP address for N3 Interface (Usually same with local IP)

- # List of AMF address information
amfConfigs:
+  - address: 192.168.64.3 #127.0.0.5
+    port: 38412

- # List of supported S-NSSAIs by this gNB
slices:
+  - sst: 1
+    sd: 0x000001
+  - sst: 1
+    sd: 0x000002

- # Indicates whether or not SCTP stream number errors should be ignored.
ignoreStreamIds: true
```



#### Changes in configuration files of UE1

```diff

- # IMSI number of the UE. IMSI = [MCC|MNC|MSISDN] (In total 15 digits)
+ supi: 'imsi-999700000000005'
- # Mobile Country Code value of HPLMN
+ mcc: '999'
- # Mobile Network Code value of HPLMN (2 or 3 digits)
+ mnc: '70'
- # SUCI Protection Scheme : 0 for Null-scheme, 1 for Profile A and 2 for Profile B
protectionScheme: 0
- # Home Network Public Key for protecting with SUCI Profile A
homeNetworkPublicKey: '5a8d38864820197c3394b92613b20b91633cbd897119273bf8e4a6f4eec0a650'
- # Home Network Public Key ID for protecting with SUCI Profile A
homeNetworkPublicKeyId: 1
- # Routing Indicator
routingIndicator: '0000'

- # Permanent subscription key
key: '465B5CE8B199B49FAA5F0A2EE238A6BC'
- # Operator code (OP or OPC) of the UE
op: 'E8ED289DEBA952E4283B54E88E6183CA'
- # This value specifies the OP type and it can be either 'OP' or 'OPC'
opType: 'OPC'
- # Authentication Management Field (AMF) value
amf: '8000'
- # IMEI number of the device. It is used if no SUPI is provided
imei: '356938035643803'
- # IMEISV number of the device. It is used if no SUPI and IMEI is provided
imeiSv: '4370816125816151'

- # List of gNB IP addresses for Radio Link Simulation
gnbSearchList:
+  - 192.168.64.5

- # UAC Access Identities Configuration
uacAic:
  mps: false
  mcs: false

- # UAC Access Control Class
uacAcc:
  normalClass: 0
  class11: false
  class12: false
  class13: false
  class14: false
  class15: false

- # Initial PDU sessions to be established
sessions:
+  - type: 'IPv4'
+    apn: 'internet'
+    slice:
+      sst: 1
+      sd: 0x000001

- # Configured NSSAI for this UE by HPLMN
configured-nssai:
+  - sst: 1
+    sd: 0x000001

- # Default Configured NSSAI for this UE
default-nssai:
+  - sst: 1
+    sd: 0x000001

- # Supported integrity algorithms by this UE
integrity:
  IA1: true
  IA2: true
  IA3: true

- # Supported encryption algorithms by this UE
ciphering:
  EA1: true
  EA2: true
  EA3: true

- # Integrity protection maximum data rate for user plane
integrityMaxRate:
  uplink: 'full'
  downlink: 'full'
```


#### Changes in configuration files of UE2
```diff
- # IMSI number of the UE. IMSI = [MCC|MNC|MSISDN] (In total 15 digits)
+ supi: 'imsi-999700000000006'
- # Mobile Country Code value of HPLMN
+ mcc: '999'
- # Mobile Network Code value of HPLMN (2 or 3 digits)
+ mnc: '70'
- # SUCI Protection Scheme : 0 for Null-scheme, 1 for Profile A and 2 for Profile B
protectionScheme: 0
- # Home Network Public Key for protecting with SUCI Profile A
homeNetworkPublicKey: '5a8d38864820197c3394b92613b20b91633cbd897119273bf8e4a6f4eec0a650'
- # Home Network Public Key ID for protecting with SUCI Profile A
homeNetworkPublicKeyId: 1
- # Routing Indicator
routingIndicator: '0000'

- # Permanent subscription key
key: '465B5CE8B199B49FAA5F0A2EE238A6BC'
- # Operator code (OP or OPC) of the UE
op: 'E8ED289DEBA952E4283B54E88E6183CA'
- # This value specifies the OP type and it can be either 'OP' or 'OPC'
opType: 'OPC'
- # Authentication Management Field (AMF) value
amf: '8000'
- # IMEI number of the device. It is used if no SUPI is provided
imei: '356938035643803'
- # IMEISV number of the device. It is used if no SUPI and IMEI is provided
imeiSv: '4370816125816151'

- # List of gNB IP addresses for Radio Link Simulation
gnbSearchList:
+  - 192.168.64.5

- # UAC Access Identities Configuration
uacAic:
  mps: false
  mcs: false

- # UAC Access Control Class
uacAcc:
  normalClass: 0
  class11: false
  class12: false
  class13: false
  class14: false
  class15: false

- # Initial PDU sessions to be established
sessions:
 + - type: 'IPv4'
 +   apn: 'internet'
 +   slice:
 +     sst: 1

- # Configured NSSAI for this UE by HPLMN
+ configured-nssai:
+  - sst: 1

- # Default Configured NSSAI for this UE
+ default-nssai:
+  - sst: 1
+    sd: 1

- # Supported integrity algorithms by this UE
integrity:
  IA1: true
  IA2: true
  IA3: true

- # Supported encryption algorithms by this UE
ciphering:
  EA1: true
  EA2: true
  EA3: true

- # Integrity protection maximum data rate for user plane
integrityMaxRate:
  uplink: 'full'
  downlink: 'full'
```

<a id="network_settings"></a>




### Configuration changes for Voip call
#### Changes in configuration files of SMF1

```diff
logger:
  file: /root/open5gs/install/var/log/open5gs/smf1.log
- #  level: info   # fatal|error|warn|info(default)|debug|trace

global:
  max:
    ue: 1024  # The number of UE can be increased depending on memory size.
- #    peer: 64

smf:
  sbi:
    server:
      - address: 127.0.0.4
        port: 7777
    client:
- #      nrf:
- #        - uri: http://127.0.0.10:7777
      scp:
        - uri: http://127.0.0.200:7777
  pfcp:
    server:
+      - address: 192.168.64.11
+        dnn: voip
    client:
      upf:
+       - address: 192.168.64.4
  gtpc:
    server:
      - address: 127.0.0.4
  gtpu:
    server:
+      - address: 192.168.64.11
  metrics:
    server:
      - address: 127.0.0.4
        port: 9090
  session:
+    - subnet: 10.45.0.1/16
+    - dnn: voip

  dns:
    - 8.8.8.8
    - 8.8.4.4
    - 2001:4860:4860::8888
    - 2001:4860:4860::8844
  mtu: 1400
- #  p-cscf:
- #    - 127.0.0.1
- #    - ::1
- #  ctf:
- #    enabled: auto   # auto(default)|yes|no
  freeDiameter: /root/open5gs/install/etc/freeDiameter/smf1.conf
  info:
+    - s_nssai:
+        - sst: 1
+         sd: 000001
+          dnn:
+            - voip
+      tai:
+        - plmn_id:
+            mcc: 999
+            mnc: 70
+          tac: 1
  pfcp:
    client:
      upf:
+        - address: 192.168.64.4
          dnn: voip
```

### Network settings of Open5GS 5GC U-Plane1

First, uncomment the next line in the `/etc/sysctl.conf` file and reflect it in the OS.
```
net.ipv4.ip_forward=1
```
```
# sysctl -p
```
Next, configure the TUNnel interface and NAPT.
```
ip tuntap add name ogstun mode tun
ip addr add 10.45.0.1/16 dev ogstun
ip link set ogstun up

iptables -t nat -A POSTROUTING -s 10.45.0.0/16 ! -o ogstun -j MASQUERADE
```

<a id="network_settings_up2"></a>


### Network settings of Open5GS 5GC U-Plane2

First, uncomment the next line in the `/etc/sysctl.conf` file and reflect it in the OS.
```
net.ipv4.ip_forward=1
```
```
# sysctl -p
```
Next, configure the TUNnel interface and NAPT.
```
ip tuntap add name ogstun mode tun
ip addr add 10.46.0.1/16 dev ogstun
ip link set ogstun up

iptables -t nat -A POSTROUTING -s 10.46.0.0/16 ! -o ogstun -j MASQUERADE
```

<a id="build"></a>

## Build Open5GS and UERANSIM

Please refer to the following for building Open5GS and UERANSIM respectively.
- Open5GS v2.6.1 (2023.03.18) - https://open5gs.org/open5gs/docs/guide/02-building-open5gs-from-sources/
- UERANSIM v3.2.6 (2023.03.17) - https://github.com/aligungr/UERANSIM/wiki/Installation

Install MongoDB on Open5GS 5GC C-Plane machine.
It is not necessary to install MongoDB on Open5GS 5GC U-Plane machines.
[MongoDB Compass](https://www.mongodb.com/products/compass) is a convenient tool to look at the MongoDB database.

<a id="run"></a>

## Run Open5GS 5GC and UERANSIM UE / RAN

First run the 5GC, then UERANSIM (UE & RAN implementation).

<a id="run_cp"></a>

### Run Open5GS 5GC C-Plane

First, run Open5GS 5GC C-Plane.

- Open5GS 5GC C-Plane

./install/bin/open5gs-nrfd &
sleep 2
./install/bin/open5gs-scpd &
sleep 2
./install/bin/open5gs-amfd &
sleep 2
./install/bin/open5gs-smfd -c install/etc/open5gs/smf1.yaml &
./install/bin/open5gs-smfd -c install/etc/open5gs/smf2.yaml &
./install/bin/open5gs-ausfd &
./install/bin/open5gs-udmd &
./install/bin/open5gs-udrd &
./install/bin/open5gs-pcfd &
./install/bin/open5gs-nssfd &
./install/bin/open5gs-bsfd &


<a id="run_up"></a>

### Run Open5GS 5GC U-Plane1 & U-Plane2

Next, run Open5GS 5GC U-Plane.

- Open5GS 5GC U-Plane1

./install/bin/open5gs-upfd &

- Open5GS 5GC U-Plane2

./install/bin/open5gs-upfd &

Then run tcpdump on one more terminal for each U-Plane.
- Run tcpdump on VM2 (U-Plane1)

# tcpdump -i ogstun -n
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on ogstun, link-type RAW (Raw IP), capture size 262144 bytes

- Run tcpdump on VM3 (U-Plane2)

# tcpdump -i ogstun -n
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on ogstun, link-type RAW (Raw IP), capture size 262144 bytes


<a id="run_ran"></a>

### Run UERANSIM (gNodeB)

Please refer to the following for usage of UERANSIM.

https://github.com/aligungr/UERANSIM/wiki/Usage


# ./nr-gnb -c ../config/open5gs-gnb.yaml
UERANSIM v3.2.6
[2023-03-18 18:31:05.057] [sctp] [info] Trying to establish SCTP connection... (192.168.0.111:38412)
[2023-03-18 18:31:05.060] [sctp] [info] SCTP connection established (192.168.0.111:38412)
[2023-03-18 18:31:05.060] [sctp] [debug] SCTP association setup ascId[6]
[2023-03-18 18:31:05.060] [ngap] [debug] Sending NG Setup Request
[2023-03-18 18:31:05.061] [ngap] [debug] NG Setup Response received
[2023-03-18 18:31:05.061] [ngap] [info] NG Setup procedure is successful

The Open5GS C-Plane log when executed is as follows.

03/18 18:31:05.062: [amf] INFO: gNB-N2 accepted[192.168.0.131]:53261 in ng-path module (../src/amf/ngap-sctp.c:113)
03/18 18:31:05.062: [amf] INFO: gNB-N2 accepted[192.168.0.131] in master_sm module (../src/amf/amf-sm.c:733)
03/18 18:31:05.062: [amf] INFO: [Added] Number of gNBs is now 1 (../src/amf/context.c:1034)
03/18 18:31:05.062: [amf] INFO: gNB-N2[192.168.0.131] max_num_of_ostreams : 10 (../src/amf/amf-sm.c:772)


<a id="run_sd1"></a>

### Run UERANSIM (UE[SST:1, SD:0x000001])

Confirm that the packet goes through the DN of U-Plane1 based on SST:1 and SD:0x000001.

<a id="con_sd1"></a>

#### UE connects to U-Plane1 based on SST:1 and SD:0x000001


# ./nr-ue -c ../config/open5gs-ue-sd1.yaml 
UERANSIM v3.2.6
[2023-03-18 18:36:26.233] [nas] [info] UE switches to state [MM-DEREGISTERED/PLMN-SEARCH]
[2023-03-18 18:36:26.234] [rrc] [debug] New signal detected for cell[1], total [1] cells in coverage
[2023-03-18 18:36:26.235] [nas] [info] Selected plmn[001/01]
[2023-03-18 18:36:26.235] [rrc] [info] Selected cell plmn[001/01] tac[1] category[SUITABLE]
[2023-03-18 18:36:26.235] [nas] [info] UE switches to state [MM-DEREGISTERED/PS]
[2023-03-18 18:36:26.236] [nas] [info] UE switches to state [MM-DEREGISTERED/NORMAL-SERVICE]
[2023-03-18 18:36:26.236] [nas] [debug] Initial registration required due to [MM-DEREG-NORMAL-SERVICE]
[2023-03-18 18:36:26.238] [nas] [debug] UAC access attempt is allowed for identity[0], category[MO_sig]
[2023-03-18 18:36:26.238] [nas] [debug] Sending Initial Registration
[2023-03-18 18:36:26.238] [rrc] [debug] Sending RRC Setup Request
[2023-03-18 18:36:26.239] [nas] [info] UE switches to state [MM-REGISTER-INITIATED]
[2023-03-18 18:36:26.239] [rrc] [info] RRC connection established
[2023-03-18 18:36:26.239] [rrc] [info] UE switches to state [RRC-CONNECTED]
[2023-03-18 18:36:26.239] [nas] [info] UE switches to state [CM-CONNECTED]
[2023-03-18 18:36:26.249] [nas] [debug] Authentication Request received
[2023-03-18 18:36:26.257] [nas] [debug] Security Mode Command received
[2023-03-18 18:36:26.257] [nas] [debug] Selected integrity[2] ciphering[0]
[2023-03-18 18:36:26.277] [nas] [debug] Registration accept received
[2023-03-18 18:36:26.278] [nas] [info] UE switches to state [MM-REGISTERED/NORMAL-SERVICE]
[2023-03-18 18:36:26.278] [nas] [debug] Sending Registration Complete
[2023-03-18 18:36:26.278] [nas] [info] Initial Registration is successful
[2023-03-18 18:36:26.278] [nas] [debug] Sending PDU Session Establishment Request
[2023-03-18 18:36:26.278] [nas] [debug] UAC access attempt is allowed for identity[0], category[MO_sig]
[2023-03-18 18:36:26.482] [nas] [debug] Configuration Update Command received
[2023-03-18 18:36:26.505] [nas] [debug] PDU Session Establishment Accept received
[2023-03-18 18:36:26.508] [nas] [info] PDU Session establishment is successful PSI[1]
[2023-03-18 18:36:26.537] [app] [info] Connection setup for PDU session[1] is successful, TUN interface[uesimtun0, 10.45.0.2] is up.

The Open5GS C-Plane log when executed is as follows.

03/18 18:36:26.247: [amf] INFO: InitialUEMessage (../src/amf/ngap-handler.c:372)
03/18 18:36:26.247: [amf] INFO: [Added] Number of gNB-UEs is now 1 (../src/amf/context.c:2327)
03/18 18:36:26.247: [amf] INFO:     RAN_UE_NGAP_ID[1] AMF_UE_NGAP_ID[1] TAC[1] CellID[0x10] (../src/amf/ngap-handler.c:533)
03/18 18:36:26.247: [amf] INFO: [suci-0-001-01-0000-0-0-0000000000] Unknown UE by SUCI (../src/amf/context.c:1634)
03/18 18:36:26.247: [amf] INFO: [Added] Number of AMF-UEs is now 1 (../src/amf/context.c:1419)
03/18 18:36:26.247: [gmm] INFO: Registration request (../src/amf/gmm-sm.c:985)
03/18 18:36:26.247: [gmm] INFO: [suci-0-001-01-0000-0-0-0000000000]    SUCI (../src/amf/gmm-handler.c:149)
03/18 18:36:26.248: [sbi] WARNING: [9302d02a-c56f-41ed-9e7f-19d339c774dc] (NF-discover) NF has already been added (../lib/sbi/nnrf-handler.c:839)
03/18 18:36:26.249: [sbi] WARNING: NF EndPoint updated [127.0.0.11:80] (../lib/sbi/context.c:1618)
03/18 18:36:26.249: [sbi] WARNING: NF EndPoint updated [127.0.0.11:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.249: [sbi] INFO: [9302d02a-c56f-41ed-9e7f-19d339c774dc] (NF-discover) NF Profile updated (../lib/sbi/nnrf-handler.c:862)
03/18 18:36:26.250: [sbi] WARNING: [930336dc-c56f-41ed-8ec2-99e4d7fea96d] (NF-discover) NF has already been added (../lib/sbi/nnrf-handler.c:839)
03/18 18:36:26.250: [sbi] WARNING: NF EndPoint updated [127.0.0.12:80] (../lib/sbi/context.c:1618)
03/18 18:36:26.251: [sbi] WARNING: NF EndPoint updated [127.0.0.12:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.251: [sbi] WARNING: NF EndPoint updated [127.0.0.12:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.251: [sbi] WARNING: NF EndPoint updated [127.0.0.12:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.251: [sbi] INFO: [930336dc-c56f-41ed-8ec2-99e4d7fea96d] (NF-discover) NF Profile updated (../lib/sbi/nnrf-handler.c:862)
03/18 18:36:26.266: [sbi] WARNING: [930336dc-c56f-41ed-8ec2-99e4d7fea96d] (NF-discover) NF has already been added (../lib/sbi/nnrf-handler.c:839)
03/18 18:36:26.267: [sbi] WARNING: NF EndPoint updated [127.0.0.12:80] (../lib/sbi/context.c:1618)
03/18 18:36:26.267: [sbi] WARNING: NF EndPoint updated [127.0.0.12:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.267: [sbi] WARNING: NF EndPoint updated [127.0.0.12:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.267: [sbi] WARNING: NF EndPoint updated [127.0.0.12:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.267: [sbi] INFO: [930336dc-c56f-41ed-8ec2-99e4d7fea96d] (NF-discover) NF Profile updated (../lib/sbi/nnrf-handler.c:862)
03/18 18:36:26.270: [sbi] WARNING: [930336dc-c56f-41ed-8ec2-99e4d7fea96d] (NF-discover) NF has already been added (../lib/sbi/nnrf-handler.c:839)
03/18 18:36:26.270: [sbi] WARNING: NF EndPoint updated [127.0.0.12:80] (../lib/sbi/context.c:1618)
03/18 18:36:26.271: [sbi] WARNING: NF EndPoint updated [127.0.0.12:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.271: [sbi] WARNING: NF EndPoint updated [127.0.0.12:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.271: [sbi] WARNING: NF EndPoint updated [127.0.0.12:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.271: [sbi] INFO: [930336dc-c56f-41ed-8ec2-99e4d7fea96d] (NF-discover) NF Profile updated (../lib/sbi/nnrf-handler.c:862)
03/18 18:36:26.278: [sbi] WARNING: [930b3c88-c56f-41ed-a613-a1f4abd59bcf] (NF-discover) NF has already been added (../lib/sbi/nnrf-handler.c:839)
03/18 18:36:26.278: [sbi] WARNING: NF EndPoint updated [127.0.0.13:80] (../lib/sbi/context.c:1618)
03/18 18:36:26.279: [sbi] WARNING: NF EndPoint updated [127.0.0.13:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.279: [sbi] WARNING: NF EndPoint updated [127.0.0.13:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.279: [sbi] WARNING: NF EndPoint updated [127.0.0.13:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.279: [sbi] INFO: [930b3c88-c56f-41ed-a613-a1f4abd59bcf] (NF-discover) NF Profile updated (../lib/sbi/nnrf-handler.c:862)
03/18 18:36:26.281: [sbi] WARNING: [930b9886-c56f-41ed-bfe8-971da2896416] (NF-discover) NF has already been added (../lib/sbi/nnrf-handler.c:839)
03/18 18:36:26.281: [sbi] WARNING: NF EndPoint updated [127.0.0.20:80] (../lib/sbi/context.c:1618)
03/18 18:36:26.282: [sbi] WARNING: NF EndPoint updated [127.0.0.20:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.282: [sbi] INFO: [930b9886-c56f-41ed-bfe8-971da2896416] (NF-discover) NF Profile updated (../lib/sbi/nnrf-handler.c:862)
03/18 18:36:26.486: [gmm] INFO: [imsi-001010000000000] Registration complete (../src/amf/gmm-sm.c:1917)
03/18 18:36:26.486: [amf] INFO: [imsi-001010000000000] Configuration update command (../src/amf/nas-path.c:612)
03/18 18:36:26.487: [gmm] INFO:     UTC [2023-03-18T09:36:26] Timezone[0]/DST[0] (../src/amf/gmm-build.c:545)
03/18 18:36:26.487: [gmm] INFO:     LOCAL [2023-03-18T18:36:26] Timezone[32400]/DST[0] (../src/amf/gmm-build.c:550)
03/18 18:36:26.489: [amf] INFO: [Added] Number of AMF-Sessions is now 1 (../src/amf/context.c:2348)
03/18 18:36:26.489: [gmm] INFO: UE SUPI[imsi-001010000000000] DNN[internet] S_NSSAI[SST:1 SD:0x1] (../src/amf/gmm-handler.c:1186)
03/18 18:36:26.492: [smf] INFO: [Added] Number of SMF-UEs is now 1 (../src/smf/context.c:1012)
03/18 18:36:26.493: [smf] INFO: [Added] Number of SMF-Sessions is now 1 (../src/smf/context.c:3108)
03/18 18:36:26.496: [sbi] WARNING: [930336dc-c56f-41ed-8ec2-99e4d7fea96d] (NF-discover) NF has already been added (../lib/sbi/nnrf-handler.c:839)
03/18 18:36:26.496: [sbi] WARNING: NF EndPoint updated [127.0.0.12:80] (../lib/sbi/context.c:1618)
03/18 18:36:26.496: [sbi] WARNING: NF EndPoint updated [127.0.0.12:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.496: [sbi] WARNING: NF EndPoint updated [127.0.0.12:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.496: [sbi] WARNING: NF EndPoint updated [127.0.0.12:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.496: [sbi] INFO: [930336dc-c56f-41ed-8ec2-99e4d7fea96d] (NF-discover) NF Profile updated (../lib/sbi/nnrf-handler.c:862)
03/18 18:36:26.500: [sbi] WARNING: [930b3c88-c56f-41ed-a613-a1f4abd59bcf] (NF-discover) NF has already been added (../lib/sbi/nnrf-handler.c:839)
03/18 18:36:26.500: [sbi] WARNING: NF EndPoint updated [127.0.0.13:80] (../lib/sbi/context.c:1618)
03/18 18:36:26.500: [sbi] WARNING: NF EndPoint updated [127.0.0.13:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.501: [sbi] WARNING: NF EndPoint updated [127.0.0.13:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.501: [sbi] WARNING: NF EndPoint updated [127.0.0.13:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.501: [sbi] INFO: [930b3c88-c56f-41ed-a613-a1f4abd59bcf] (NF-discover) NF Profile updated (../lib/sbi/nnrf-handler.c:862)
03/18 18:36:26.502: [sbi] WARNING: [930b9886-c56f-41ed-bfe8-971da2896416] (NF-discover) NF has already been added (../lib/sbi/nnrf-handler.c:839)
03/18 18:36:26.503: [sbi] WARNING: NF EndPoint updated [127.0.0.20:80] (../lib/sbi/context.c:1618)
03/18 18:36:26.503: [sbi] WARNING: NF EndPoint updated [127.0.0.20:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.503: [sbi] INFO: [930b9886-c56f-41ed-bfe8-971da2896416] (NF-discover) NF Profile updated (../lib/sbi/nnrf-handler.c:862)
03/18 18:36:26.505: [sbi] WARNING: [9303a4aa-c56f-41ed-9f51-cb823d86c4c9] (NF-discover) NF has already been added (../lib/sbi/nnrf-handler.c:839)
03/18 18:36:26.505: [sbi] WARNING: NF EndPoint updated [127.0.0.15:80] (../lib/sbi/context.c:1618)
03/18 18:36:26.505: [sbi] WARNING: NF EndPoint updated [127.0.0.15:7777] (../lib/sbi/context.c:1527)
03/18 18:36:26.505: [sbi] INFO: [9303a4aa-c56f-41ed-9f51-cb823d86c4c9] (NF-discover) NF Profile updated (../lib/sbi/nnrf-handler.c:862)
03/18 18:36:26.507: [smf] INFO: UE SUPI[imsi-001010000000000] DNN[internet] IPv4[10.45.0.2] IPv6[] (../src/smf/npcf-handler.c:528)
03/18 18:36:26.508: [gtp] INFO: gtp_connect() [192.168.0.114]:2152 (../lib/gtp/path.c:60)

The Open5GS U-Plane1 log when executed is as follows.

03/18 18:36:26.517: [upf] INFO: [Added] Number of UPF-Sessions is now 1 (../src/upf/context.c:194)
03/18 18:36:26.517: [gtp] INFO: gtp_connect() [192.168.0.112]:2152 (../lib/gtp/path.c:60)
03/18 18:36:26.517: [upf] INFO: UE F-SEID[UP:0x1 CP:0x1] APN[internet] PDN-Type[1] IPv4[10.45.0.2] IPv6[] (../src/upf/context.c:467)
03/18 18:36:26.517: [upf] INFO: UE F-SEID[UP:0x1 CP:0x1] APN[internet] PDN-Type[1] IPv4[10.45.0.2] IPv6[] (../src/upf/context.c:467)
03/18 18:36:26.522: [gtp] INFO: gtp_connect() [192.168.0.131]:2152 (../lib/gtp/path.c:60)

The TUNnel interface uesimtun0 is created as follows.

# ip addr show
...
8: uesimtun0: <POINTOPOINT,PROMISC,NOTRAILERS,UP,LOWER_UP> mtu 1400 qdisc fq_codel state UNKNOWN group default qlen 500
    link/none 
    inet 10.45.0.2/32 scope global uesimtun0
       valid_lft forever preferred_lft forever
    inet6 fe80::72b5:9b5:1c5a:f233/64 scope link stable-privacy 
       valid_lft forever preferred_lft forever
...


<a id="ping_sd1"></a>

#### Ping google.com going through DN=10.45.0.0/16 on U-Plane1

Confirm by using tcpdump that the packet goes through if=ogstun on U-Plane1.

# ping google.com -I uesimtun0 -n
PING google.com (142.250.199.110) from 10.45.0.2 uesimtun0: 56(84) bytes of data.
64 bytes from 142.250.199.110: icmp_seq=1 ttl=61 time=23.3 ms
64 bytes from 142.250.199.110: icmp_seq=2 ttl=61 time=19.7 ms
64 bytes from 142.250.199.110: icmp_seq=3 ttl=61 time=20.4 ms

The tcpdump log on U-Plane1 is as follows.

18:39:57.087028 IP 10.45.0.2 > 142.250.199.110: ICMP echo request, id 8, seq 1, length 64
18:39:57.108163 IP 142.250.199.110 > 10.45.0.2: ICMP echo reply, id 8, seq 1, length 64
18:39:58.087725 IP 10.45.0.2 > 142.250.199.110: ICMP echo request, id 8, seq 2, length 64
18:39:58.105485 IP 142.250.199.110 > 10.45.0.2: ICMP echo reply, id 8, seq 2, length 64
18:39:59.088981 IP 10.45.0.2 > 142.250.199.110: ICMP echo request, id 8, seq 3, length 64
18:39:59.107326 IP 142.250.199.110 > 10.45.0.2: ICMP echo reply, id 8, seq 3, length 64

*Note. Make sure the packet does not go through U-Plane2.*

<a id="run_sd2"></a>

### Run UERANSIM (UE[SST:1, SD:0x000002])

Then the UE disconnects from gNodeB and connects to gNodeB using the configuration file for SST:1 and SD:0x000002.
Confirm that the packet goes through the DN of U-Plane2 based on SST:1 and SD:0x000002.

<a id="con_sd2"></a>

#### UE connects to U-Plane2 based on SST:1 and SD:0x000002


# ./nr-ue -c ../config/open5gs-ue-sd2.yaml 
UERANSIM v3.2.6
[2023-03-18 18:44:07.238] [nas] [info] UE switches to state [MM-DEREGISTERED/PLMN-SEARCH]
[2023-03-18 18:44:07.239] [rrc] [debug] New signal detected for cell[1], total [1] cells in coverage
[2023-03-18 18:44:07.239] [nas] [info] Selected plmn[001/01]
[2023-03-18 18:44:07.239] [rrc] [info] Selected cell plmn[001/01] tac[1] category[SUITABLE]
[2023-03-18 18:44:07.240] [nas] [info] UE switches to state [MM-DEREGISTERED/PS]
[2023-03-18 18:44:07.240] [nas] [info] UE switches to state [MM-DEREGISTERED/NORMAL-SERVICE]
[2023-03-18 18:44:07.240] [nas] [debug] Initial registration required due to [MM-DEREG-NORMAL-SERVICE]
[2023-03-18 18:44:07.242] [nas] [debug] UAC access attempt is allowed for identity[0], category[MO_sig]
[2023-03-18 18:44:07.242] [nas] [debug] Sending Initial Registration
[2023-03-18 18:44:07.242] [rrc] [debug] Sending RRC Setup Request
[2023-03-18 18:44:07.243] [nas] [info] UE switches to state [MM-REGISTER-INITIATED]
[2023-03-18 18:44:07.243] [rrc] [info] RRC connection established
[2023-03-18 18:44:07.243] [rrc] [info] UE switches to state [RRC-CONNECTED]
[2023-03-18 18:44:07.243] [nas] [info] UE switches to state [CM-CONNECTED]
[2023-03-18 18:44:07.256] [nas] [debug] Authentication Request received
[2023-03-18 18:44:07.261] [nas] [debug] Security Mode Command received
[2023-03-18 18:44:07.261] [nas] [debug] Selected integrity[2] ciphering[0]
[2023-03-18 18:44:07.273] [nas] [debug] Registration accept received
[2023-03-18 18:44:07.273] [nas] [info] UE switches to state [MM-REGISTERED/NORMAL-SERVICE]
[2023-03-18 18:44:07.273] [nas] [debug] Sending Registration Complete
[2023-03-18 18:44:07.273] [nas] [info] Initial Registration is successful
[2023-03-18 18:44:07.274] [nas] [debug] Sending PDU Session Establishment Request
[2023-03-18 18:44:07.274] [nas] [debug] UAC access attempt is allowed for identity[0], category[MO_sig]
[2023-03-18 18:44:07.481] [nas] [debug] Configuration Update Command received
[2023-03-18 18:44:07.504] [nas] [debug] PDU Session Establishment Accept received
[2023-03-18 18:44:07.508] [nas] [info] PDU Session establishment is successful PSI[1]
[2023-03-18 18:44:07.534] [app] [info] Connection setup for PDU session[1] is successful, TUN interface[uesimtun0, 10.46.0.2] is up.

The Open5GS C-Plane log when executed is as follows.

03/18 18:44:07.252: [amf] INFO: InitialUEMessage (../src/amf/ngap-handler.c:372)
03/18 18:44:07.252: [amf] INFO: [Added] Number of gNB-UEs is now 2 (../src/amf/context.c:2327)
03/18 18:44:07.252: [amf] INFO:     RAN_UE_NGAP_ID[2] AMF_UE_NGAP_ID[2] TAC[1] CellID[0x10] (../src/amf/ngap-handler.c:533)
03/18 18:44:07.252: [amf] INFO: [suci-0-001-01-0000-0-0-0000000000] known UE by SUCI (../src/amf/context.c:1632)
03/18 18:44:07.252: [gmm] INFO: Registration request (../src/amf/gmm-sm.c:985)
03/18 18:44:07.252: [gmm] INFO: [suci-0-001-01-0000-0-0-0000000000]    SUCI (../src/amf/gmm-handler.c:149)
03/18 18:44:07.253: [amf] INFO: UE Context Release [Action:1] (../src/amf/ngap-handler.c:1632)
03/18 18:44:07.253: [amf] INFO:     RAN_UE_NGAP_ID[1] AMF_UE_NGAP_ID[1] (../src/amf/ngap-handler.c:1633)
03/18 18:44:07.253: [amf] INFO: [Removed] Number of gNB-UEs is now 1 (../src/amf/context.c:2334)
03/18 18:44:07.257: [smf] INFO: Removed Session: UE IMSI:[imsi-001010000000000] DNN:[internet:1] IPv4:[10.45.0.2] IPv6:[] (../src/smf/context.c:1710)
03/18 18:44:07.257: [smf] INFO: [Removed] Number of SMF-Sessions is now 0 (../src/smf/context.c:3116)
03/18 18:44:07.257: [smf] INFO: [Removed] Number of SMF-UEs is now 0 (../src/smf/context.c:1071)
03/18 18:44:07.258: [amf] INFO: [imsi-001010000000000:1] Release SM context [204] (../src/amf/amf-sm.c:491)
03/18 18:44:07.258: [amf] INFO: [Removed] Number of AMF-Sessions is now 0 (../src/amf/context.c:2355)
03/18 18:44:07.277: [pcf] WARNING: NF EndPoint updated [127.0.0.5:7777] (../src/pcf/npcf-handler.c:100)
03/18 18:44:07.485: [gmm] INFO: [imsi-001010000000000] Registration complete (../src/amf/gmm-sm.c:1917)
03/18 18:44:07.486: [amf] INFO: [imsi-001010000000000] Configuration update command (../src/amf/nas-path.c:612)
03/18 18:44:07.486: [gmm] INFO:     UTC [2023-03-18T09:44:07] Timezone[0]/DST[0] (../src/amf/gmm-build.c:545)
03/18 18:44:07.487: [gmm] INFO:     LOCAL [2023-03-18T18:44:07] Timezone[32400]/DST[0] (../src/amf/gmm-build.c:550)
03/18 18:44:07.487: [amf] INFO: [Added] Number of AMF-Sessions is now 1 (../src/amf/context.c:2348)
03/18 18:44:07.488: [gmm] INFO: UE SUPI[imsi-001010000000000] DNN[internet] S_NSSAI[SST:1 SD:0x2] (../src/amf/gmm-handler.c:1186)
03/18 18:44:07.491: [smf] INFO: [Added] Number of SMF-UEs is now 1 (../src/smf/context.c:1012)
03/18 18:44:07.491: [smf] INFO: [Added] Number of SMF-Sessions is now 1 (../src/smf/context.c:3108)
03/18 18:44:07.494: [sbi] WARNING: [930336dc-c56f-41ed-8ec2-99e4d7fea96d] (NF-discover) NF has already been added (../lib/sbi/nnrf-handler.c:839)
03/18 18:44:07.495: [sbi] WARNING: NF EndPoint updated [127.0.0.12:80] (../lib/sbi/context.c:1618)
03/18 18:44:07.495: [sbi] WARNING: NF EndPoint updated [127.0.0.12:7777] (../lib/sbi/context.c:1527)
03/18 18:44:07.495: [sbi] WARNING: NF EndPoint updated [127.0.0.12:7777] (../lib/sbi/context.c:1527)
03/18 18:44:07.495: [sbi] WARNING: NF EndPoint updated [127.0.0.12:7777] (../lib/sbi/context.c:1527)
03/18 18:44:07.495: [sbi] INFO: [930336dc-c56f-41ed-8ec2-99e4d7fea96d] (NF-discover) NF Profile updated (../lib/sbi/nnrf-handler.c:862)
03/18 18:44:07.499: [sbi] WARNING: [930b3c88-c56f-41ed-a613-a1f4abd59bcf] (NF-discover) NF has already been added (../lib/sbi/nnrf-handler.c:839)
03/18 18:44:07.499: [sbi] WARNING: NF EndPoint updated [127.0.0.13:80] (../lib/sbi/context.c:1618)
03/18 18:44:07.500: [sbi] WARNING: NF EndPoint updated [127.0.0.13:7777] (../lib/sbi/context.c:1527)
03/18 18:44:07.500: [sbi] WARNING: NF EndPoint updated [127.0.0.13:7777] (../lib/sbi/context.c:1527)
03/18 18:44:07.500: [sbi] WARNING: NF EndPoint updated [127.0.0.13:7777] (../lib/sbi/context.c:1527)
03/18 18:44:07.500: [sbi] INFO: [930b3c88-c56f-41ed-a613-a1f4abd59bcf] (NF-discover) NF Profile updated (../lib/sbi/nnrf-handler.c:862)
03/18 18:44:07.502: [sbi] WARNING: [930b9886-c56f-41ed-bfe8-971da2896416] (NF-discover) NF has already been added (../lib/sbi/nnrf-handler.c:839)
03/18 18:44:07.502: [sbi] WARNING: NF EndPoint updated [127.0.0.20:80] (../lib/sbi/context.c:1618)
03/18 18:44:07.502: [sbi] WARNING: NF EndPoint updated [127.0.0.20:7777] (../lib/sbi/context.c:1527)
03/18 18:44:07.502: [sbi] INFO: [930b9886-c56f-41ed-bfe8-971da2896416] (NF-discover) NF Profile updated (../lib/sbi/nnrf-handler.c:862)
03/18 18:44:07.504: [sbi] WARNING: [9303a4aa-c56f-41ed-9f51-cb823d86c4c9] (NF-discover) NF has already been added (../lib/sbi/nnrf-handler.c:839)
03/18 18:44:07.504: [sbi] WARNING: NF EndPoint updated [127.0.0.15:80] (../lib/sbi/context.c:1618)
03/18 18:44:07.505: [sbi] WARNING: NF EndPoint updated [127.0.0.15:7777] (../lib/sbi/context.c:1527)
03/18 18:44:07.505: [sbi] INFO: [9303a4aa-c56f-41ed-9f51-cb823d86c4c9] (NF-discover) NF Profile updated (../lib/sbi/nnrf-handler.c:862)
03/18 18:44:07.507: [smf] INFO: UE SUPI[imsi-001010000000000] DNN[internet] IPv4[10.46.0.2] IPv6[] (../src/smf/npcf-handler.c:528)
03/18 18:44:07.507: [gtp] INFO: gtp_connect() [192.168.0.115]:2152 (../lib/gtp/path.c:60)

The Open5GS U-Plane2 log when executed is as follows.

03/18 18:44:07.518: [upf] INFO: [Added] Number of UPF-Sessions is now 1 (../src/upf/context.c:194)
03/18 18:44:07.518: [gtp] INFO: gtp_connect() [192.168.0.113]:2152 (../lib/gtp/path.c:60)
03/18 18:44:07.518: [upf] INFO: UE F-SEID[UP:0x1 CP:0x1] APN[internet] PDN-Type[1] IPv4[10.46.0.2] IPv6[] (../src/upf/context.c:467)
03/18 18:44:07.518: [upf] INFO: UE F-SEID[UP:0x1 CP:0x1] APN[internet] PDN-Type[1] IPv4[10.46.0.2] IPv6[] (../src/upf/context.c:467)
03/18 18:44:07.523: [gtp] INFO: gtp_connect() [192.168.0.131]:2152 (../lib/gtp/path.c:60)

The TUNnel interface uesimtun0 is created as follows.

# ip addr show
...
9: uesimtun0: <POINTOPOINT,PROMISC,NOTRAILERS,UP,LOWER_UP> mtu 1400 qdisc fq_codel state UNKNOWN group default qlen 500
    link/none 
    inet 10.46.0.2/32 scope global uesimtun0
       valid_lft forever preferred_lft forever
    inet6 fe80::1aec:c1c3:5c4d:4720/64 scope link stable-privacy 
       valid_lft forever preferred_lft forever
...


<a id="ping_sd2"></a>

#### Ping google.com going through DN=10.46.0.0/16 on U-Plane2

Confirm by using tcpdump that the packet goes through if=ogstun on U-Plane2.

# ping google.com -I uesimtun0 -n
PING google.com (142.250.196.142) from 10.46.0.2 uesimtun0: 56(84) bytes of data.
64 bytes from 142.250.196.142: icmp_seq=1 ttl=61 time=18.8 ms
64 bytes from 142.250.196.142: icmp_seq=2 ttl=61 time=18.1 ms
64 bytes from 142.250.196.142: icmp_seq=3 ttl=61 time=18.6 ms

The tcpdump log on U-Plane2 is as follows.

18:46:32.181964 IP 10.46.0.2 > 142.250.196.142: ICMP echo request, id 9, seq 1, length 64
18:46:32.198816 IP 142.250.196.142 > 10.46.0.2: ICMP echo reply, id 9, seq 1, length 64
18:46:33.182450 IP 10.46.0.2 > 142.250.196.142: ICMP echo request, id 9, seq 2, length 64
18:46:33.198394 IP 142.250.196.142 > 10.46.0.2: ICMP echo reply, id 9, seq 2, length 64
18:46:34.183793 IP 10.46.0.2 > 142.250.196.142: ICMP echo request, id 9, seq 3, length 64
18:46:34.200004 IP 142.250.196.142 > 10.46.0.2: ICMP echo reply, id 9, seq 3, length 64

*Note. Make sure the packet does not go through U-Plane1.*

---
I was able to confirm the very simple configuration in which one UE connects to the UPF based on S-NSSAI. I would like to thank the excellent developers and all the contributors of Open5GS and UERANSIM.

<a id="changelog"></a>

## Changelog (summary)

- [2023.03.18] Updated to Open5GS v2.6.1 (2023.03.18) and UERANSIM v3.2.6 (2023.03.17).
- [2023.01.13] Updated to Open5GS v2.5.6.
- [2022.08.01] Initial release.
