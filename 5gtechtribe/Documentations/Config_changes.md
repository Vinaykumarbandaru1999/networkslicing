# Changes in configuration files of Open5GS and UERANSIM UE / RAN
 
## Changes in configuration files of Open5GS 5GC C-Plane
- To run amf
  ```bash
  ./install/bin/open5gs-amfd
  ```
- `open5gs/install/etc/open5gs/amf.yaml`
 
 
```bash
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
+        - sst: 2
+          sd: 000001
+        - sst: 2
+          sd: 000002
+        - sst: 2
+          sd: 000003
 
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
## Changes in configuration files of NSSF
```bash
logger:
  file: /root/open5gs/install/var/log/open5gs/nssf.log
#  level: info   # fatal|error|warn|info(default)|debug|trace
 
global:
  max:
    ue: 1024  # The number of UE can be increased depending on memory size.
#    peer: 64
 
nssf:
  sbi:
    server:
      - address: 127.0.0.14
        port: 7777
    client:
#      nrf:
#        - uri: http://127.0.0.10:7777
      scp:
        - uri: http://127.0.0.200:7777
      nsi:
        - uri: http://127.0.0.10:7777
          s_nssai:
            sst: 1
            sd: 000001
        - addr: 127.0.0.10
          port: 7777
          s_nssai:
            sst: 1
            sd: 000002
        - addr: 127.0.0.10
          port: 7777
          s_nssai:
            sst: 2
            sd: 000001    
        - addr: 127.0.0.10
          port: 7777
          s_nssai:
            sst: 2
            sd: 000002
        - addr: 127.0.0.10
          port: 7777
          s_nssai:
            sst: 2
            sd: 000003
        - addr: 127.0.0.10
```
 
## Changes in configuration files of SMF
### Changes in configuration files of SMF1
- To initialize the configuration file
  ```bash
  ./install/bin/open5gs-smfd -c install/etc/open5gs/smf1.yaml
  ```
- `open5gs/install/etc/open5gs/smf1.yaml`
 
```bash
logger:
  file: /root/open5gs/install/var/log/open5gs/smf1.log
 
global:
  max:
    ue: 1024
 
smf:
  sbi:
    server:
      - address: 127.0.0.4
        port: 7777
    client:
      scp:
        - uri: http://127.0.0.200:7777
  pfcp:
    server:
      - address: 192.168.64.11
    client:
      upf:
        - address: 192.168.64.4
          dnn: voip
          dnn: internet
  gtpc:
    server:
      - address: 127.0.0.4
  gtpu:
    server:
      - address: 192.168.64.11
  metrics:
    server:
      - address: 127.0.0.4
        port: 9090
  session:
    - subnet: 10.45.0.1/16
      dnn: voip
    - subnet: 10.47.0.1/16
      dnn: internet
 
  dns:
    - 8.8.8.8
    - 8.8.4.4
  mtu: 1400
  freeDiameter: /root/open5gs/install/etc/freeDiameter/smf1.conf
  info:
    - s_nssai:
        - sst: 1
          sd: 000001
          dnn:
            - voip
        - sst: 2
          sd: 000001
          dnn:
            - internet
      tai:
        - plmn_id:
            mcc: 999
            mnc: 70
          tac: 1
```
 
### Changes in configuration files of SMF2
- - To initialize the configuration file
  ```bash
  ./install/bin/open5gs-smfd -c install/etc/open5gs/smf2.yaml
  ```
- `open5gs/install/etc/open5gs/smf2.yaml`
 
 
```bash
logger:
  file: /root/open5gs/install/var/log/open5gs/smf2.log
#  level: info   # fatal|error|warn|info(default)|debug|trace
 
global:
  max:
    ue: 1024  # The number of UE can be increased depending on memory size.
#    peer: 64
 
smf:
  sbi:
    server:
      - address: 127.0.0.24
        port: 7777
    client:
#      nrf:
#        - uri: http://127.0.0.10:7777
      scp:
        - uri: http://127.0.0.200:7777
  pfcp:
    server:
      - address: 192.168.64.12
        dnn: voip
    client:
      upf:
        - address: 192.168.64.6
          dnn: voip
  gtpc:
    server:
      - address: 127.0.0.24
  gtpu:
    server:
      - address: 192.168.64.12
  metrics:
    server:
      - address: 127.0.0.24
        port: 9090
  session:
    - subnet: 10.46.0.1/16
    - dnn: voip
 
  dns:
    - 8.8.8.8
    - 8.8.4.4
    - 2001:4860:4860::8888
    - 2001:4860:4860::8844
  mtu: 1400
 
  freeDiameter: /root/open5gs/install/etc/freeDiameter/smf2.conf
  info:
    - s_nssai:
        - sst: 1
          sd: 000002
          dnn:
            - voip
      tai:
        - plmn_id:
            mcc: 999
            mnc: 70
          tac: 1
```
- `open5gs/install/etc/freeDiameter/smf2.conf`
- `smf1.conf` is equal to the original `smf.conf`.
  ```bash
  ##  Endpoint configuration
 
  # Disable use of IP addresses (only IPv6)
  # Default : IP enabled
  #No_IP;
 
  # Disable use of IPv6 addresses (only IP)
  # Default : IPv6 enabled
  #No_IPv6;
 
  # Specify local addresses the server must bind to
  # Default : listen on all addresses available.
  #ListenOn = "202.249.37.5";
  #ListenOn = "2001:200:903:2::202:1";
  #ListenOn = "fe80::21c:5ff:fe98:7d62%eth0";
  ListenOn = "127.0.0.24";
  ```
 
 
### Changes in configuration files of SMF3
- To initialize the configuration file
  ```bash
  ./install/bin/open5gs-smfd -c install/etc/open5gs/smf3.yaml
  ```
- `open5gs/install/etc/open5gs/smf3.yaml`
 
```bash
logger:
  file: /root/open5gs/install/var/log/open5gs/smf3.log
 
global:
  max:
    ue: 1024
 
smf:
  sbi:
    server:
      - address: 127.0.0.28
        port: 7777
    client:
      scp:
        - uri: http://127.0.0.200:7777
  pfcp:
    server:
      - address: 192.168.64.13
    client:
      upf:
        - address: 192.168.64.7
          dnn: internet
          dnn: internet2
  gtpc:
    server:
      - address: 127.0.0.28
  gtpu:
    server:
      - address: 192.168.64.13
  metrics:
    server:
      - address: 127.0.0.28
        port: 9090
  session:
    - subnet: 10.47.0.1/16
      dnn: internet
    - subnet: 10.48.0.1/16
      dnn: internet2
 
  dns:
    - 8.8.8.8
    - 8.8.4.4
  mtu: 1400
  freeDiameter: /root/open5gs/install/etc/freeDiameter/smf3.conf
  info:
    - s_nssai:
        - sst: 2
          sd: 000002
          dnn:
            - internet
        - sst: 2
          sd: 000003
          dnn:
            - internet2
      tai:
        - plmn_id:
            mcc: 999
            mnc: 70
          tac: 1
```
- `open5gs/install/etc/freeDiameter/smf3.conf`
 
  ```bash
  ##  Endpoint configuration
 
  # Disable use of IP addresses (only IPv6)
  # Default : IP enabled
  #No_IP;
 
  # Disable use of IPv6 addresses (only IP)
  # Default : IPv6 enabled
  #No_IPv6;
 
  # Specify local addresses the server must bind to
  # Default : listen on all addresses available.
  #ListenOn = "202.249.37.5";
  #ListenOn = "2001:200:903:2::202:1";
  #ListenOn = "fe80::21c:5ff:fe98:7d62%eth0";
  ListenOn = "127.0.0.28";
  ```
 
## configuration files of Open5GS U-Plane
### Changes in configuration files of Open5GS U-Plane1
- To excute the configuration file
  ```bash
  ./install/bin/open5gs-upfd
  ```
- `open5gs/install/etc/open5gs/upf1.yaml`
 
```bash
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
      dnn: voip
      dev: ogstun
    - subnet: 10.47.0.1/16
      dnn: internet
      dev: ogstun
  metrics:
    server:
      - address: 127.0.0.7
        port: 9090
```
 
### Changes in configuration files of Open5GS U-Plane2
- To excute the configuration file
  ```bash
  ./install/bin/open5gs-upfd
  ```
- `open5gs/install/etc/open5gs/upf2.yaml`
 
```bash
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
      dnn: voip
      dev: ogstun
  metrics:
    server:
      - address: 127.0.0.7
        port: 9090
```
 
### Changes in configuration files of Open5GS U-Plane3
- To excute the configuration file
  ```bash
  ./install/bin/open5gs-upfd
  ```
- `open5gs/install/etc/open5gs/upf3.yaml`
 
```bash
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
      - address: 192.168.64.7
 
  gtpu:
    server:
      - address: 192.168.64.7
  session:
    - subnet: 10.47.0.1/16
      dnn: internet
      dev: ogstun
    - subnet: 10.48.0.1/16
      dnn: internet2
      dev: ogstun2      
  metrics:
    server:
      - address: 127.0.0.7
        port: 9090
```
 
 
## Changes in configuration files of UERANSIM UE / RAN(GNB)
 
### Changes in configuration files of GNB1 (gNodeB1)
- To excute the configuration file
  ```bash
  sudo build/nr-gnb -c config/open5gs-gnb1.yaml
  ```
- `UERANSIM/config/open5gs-gnb1.yaml`
```bash
mcc: '999'          # Mobile Country Code value
mnc: '70'           # Mobile Network Code value (2 or 3 digits)
 
nci: '0x000000010'  # NR Cell Identity (36-bit)
idLength: 32        # NR gNB ID length in bits [22...32]
tac: 1              # Tracking Area Code
 
linkIp: 192.168.64.5 #127.0.0.1   # gNB's local IP address for Radio Link Simulation (Usually same with local IP)
ngapIp: 192.168.64.5 #127.0.0.1   # gNB's local IP address for N2 Interface (Usually same with local IP)
gtpIp: 192.168.64.5 #127.0.0.1    # gNB's local IP address for N3 Interface (Usually same with local IP)
 
# List of AMF address information
amfConfigs:
  - address: 192.168.64.3 #127.0.0.5
    port: 38412
 
# List of supported S-NSSAIs by this gNB
slices:
  - sst: 1
    sd: 0x000001
  - sst: 1
    sd: 0x000002
  - sst: 2
    sd: 0x000001
 
# Indicates whether or not SCTP stream number errors should be ignored.
ignoreStreamIds: true
```
 
### Changes in configuration files of GNB2 (gNodeB2)
- To excute the configuration file
  ```bash
  sudo build/nr-gnb -c config/open5gs-gnb2.yaml
  ```
- `UERANSIM/config/open5gs-gnb2.yaml`
 
 
```bash
mcc: '999'          # Mobile Country Code value
mnc: '70'           # Mobile Network Code value (2 or 3 digits)
 
nci: '0x000000010'  # NR Cell Identity (36-bit)
idLength: 32        # NR gNB ID length in bits [22...32]
tac: 1              # Tracking Area Code
 
linkIp: 192.168.64.65 #127.0.0.1   # gNB's local IP address for Radio Link Simulation (Usually same with local IP)
ngapIp: 192.168.64.65 #127.0.0.1   # gNB's local IP address for N2 Interface (Usually same with local IP)
gtpIp: 192.168.64.65 #127.0.0.1    # gNB's local IP address for N3 Interface (Usually same with local IP)
 
# List of AMF address information
amfConfigs:
  - address: 192.168.64.3 #127.0.0.5
    port: 38412
 
# List of supported S-NSSAIs by this gNB
slices:
  - sst: 1
    sd: 0x000002
# Indicates whether or not SCTP stream number errors should be ignored.
ignoreStreamIds: true
```
 
### Changes in configuration files of GNB3 (gNodeB3)
- To excute the configuration file
  ```bash
  sudo build/nr-gnb -c config/open5gs-gnb3.yaml
  ```
- `UERANSIM/config/open5gs-gnb3.yaml`
```bash
mcc: '999'          # Mobile Country Code value
mnc: '70'           # Mobile Network Code value (2 or 3 digits)
 
nci: '0x000000010'  # NR Cell Identity (36-bit)
idLength: 32        # NR gNB ID length in bits [22...32]
tac: 1              # Tracking Area Code
 
linkIp: 192.168.64.66   # gNB's local IP address for Radio Link Simulation (Usually same with local IP)
ngapIp: 192.168.64.66   # gNB's local IP address for N2 Interface (Usually same with local IP)
gtpIp: 192.168.64.66    # gNB's local IP address for N3 Interface (Usually same with local IP)
 
# List of AMF address information
amfConfigs:
  - address: 192.168.64.3
    port: 38412
 
# List of supported S-NSSAIs by this gNB
slices:
  - sst: 2
    sd: 0x000002
 
# Indicates whether or not SCTP stream number errors should be ignored.
ignoreStreamIds: true
```
### Changes in configuration files of GNB4 (gNodeB4)
- To excute the configuration file
  ```bash
  sudo build/nr-gnb -c config/open5gs-gnb4.yaml
  ```
- `UERANSIM/config/open5gs-gnb4.yaml`
```bash
mcc: '999'          # Mobile Country Code value
mnc: '70'           # Mobile Network Code value (2 or 3 digits)
 
nci: '0x000000010'  # NR Cell Identity (36-bit)
idLength: 32        # NR gNB ID length in bits [22...32]
tac: 1              # Tracking Area Code
 
linkIp: 192.168.64.67  # gNB's local IP address for Radio Link Simulation (Usually same with local IP)
ngapIp: 192.168.64.67   # gNB's local IP address for N2 Interface (Usually same with local IP)
gtpIp: 192.168.64.67    # gNB's local IP address for N3 Interface (Usually same with local IP)
 
# List of AMF address information
amfConfigs:
  - address: 192.168.64.3
    port: 38412
 
# List of supported S-NSSAIs by this gNB
slices:
  - sst: 2
    sd: 0x000003
 
# Indicates whether or not SCTP stream number errors should be ignored.
ignoreStreamIds: true
```
 
## Changes in configuration files of UE
### Changes in configuration files of UE1 (IMSI-999700000000001)
- To excute the configuration file
  ```bash
  sudo build/nr-ue -c config/open5gs-ue1.yaml
 
  ```
- `UERANSIM/config/open5gs-ue1.yaml`
```bash
# IMSI number of the UE. IMSI = [MCC|MNC|MSISDN] (In total 15 digits)
supi: 'imsi-999700000000001'
# Mobile Country Code value of HPLMN
mcc: '999'
# Mobile Network Code value of HPLMN (2 or 3 digits)
mnc: '70'
# SUCI Protection Scheme : 0 for Null-scheme, 1 for Profile A and 2 for Profile B
protectionScheme: 0
# Home Network Public Key for protecting with SUCI Profile A
homeNetworkPublicKey: '5a8d38864820197c3394b92613b20b91633cbd897119273bf8e4a6f4eec0a650'
# Home Network Public Key ID for protecting with SUCI Profile A
homeNetworkPublicKeyId: 1
# Routing Indicator
routingIndicator: '0000'
 
# Permanent subscription key
key: '465B5CE8B199B49FAA5F0A2EE238A6BC'
# Operator code (OP or OPC) of the UE
op: 'E8ED289DEBA952E4283B54E88E6183CA'
# This value specifies the OP type and it can be either 'OP' or 'OPC'
opType: 'OPC'
# Authentication Management Field (AMF) value
amf: '8000'
# IMEI number of the device. It is used if no SUPI is provided
imei: '356938035643803'
# IMEISV number of the device. It is used if no SUPI and IMEI is provided
imeiSv: '4370816125816151'
 
# List of gNB IP addresses for Radio Link Simulation
gnbSearchList:
  - 192.168.64.5
 
# UAC Access Identities Configuration
uacAic:
  mps: false
  mcs: false
 
# UAC Access Control Class
uacAcc:
  normalClass: 0
  class11: false
  class12: false
  class13: false
  class14: false
  class15: false
 
# Initial PDU sessions to be established
sessions:
  - type: 'IPv4'
    apn: 'voip'
    slice:
      sst: 1
      sd: 0x000001
 
# Configured NSSAI for this UE by HPLMN
configured-nssai:
  - sst: 1
    sd: 0x000001
 
# Default Configured NSSAI for this UE
default-nssai:
  - sst: 1
    sd: 0x000001
 
# Supported integrity algorithms by this UE
integrity:
  IA1: true
  IA2: true
  IA3: true
 
# Supported encryption algorithms by this UE
ciphering:
  EA1: true
  EA2: true
  EA3: true
 
# Integrity protection maximum data rate for user plane
integrityMaxRate:
  uplink: 'full'
  downlink: 'full'
```
 
### Changes in configuration files of UE2 (IMSI-999700000000002)
- To excute the configuration file
  ```bash
  sudo build/nr-ue -c config/open5gs-ue2.yaml
 
  ```
- `UERANSIM/config/open5gs-ue2.yaml`
```bash
# IMSI number of the UE. IMSI = [MCC|MNC|MSISDN] (In total 15 digits)
supi: 'imsi-999700000000002'
# Mobile Country Code value of HPLMN
mcc: '999'
# Mobile Network Code value of HPLMN (2 or 3 digits)
mnc: '70'
# SUCI Protection Scheme : 0 for Null-scheme, 1 for Profile A and 2 for Profile B
protectionScheme: 0
# Home Network Public Key for protecting with SUCI Profile A
homeNetworkPublicKey: '5a8d38864820197c3394b92613b20b91633cbd897119273bf8e4a6f4eec0a650'
# Home Network Public Key ID for protecting with SUCI Profile A
homeNetworkPublicKeyId: 1
# Routing Indicator
routingIndicator: '0000'
 
# Permanent subscription key
key: '465B5CE8B199B49FAA5F0A2EE238A6BC'
# Operator code (OP or OPC) of the UE
op: 'E8ED289DEBA952E4283B54E88E6183CA'
# This value specifies the OP type and it can be either 'OP' or 'OPC'
opType: 'OPC'
# Authentication Management Field (AMF) value
amf: '8000'
# IMEI number of the device. It is used if no SUPI is provided
imei: '356938035643803'
# IMEISV number of the device. It is used if no SUPI and IMEI is provided
imeiSv: '4370816125816151'
 
# List of gNB IP addresses for Radio Link Simulation
gnbSearchList:
  - 192.168.64.65
 
# UAC Access Identities Configuration
uacAic:
  mps: false
  mcs: false
 
# UAC Access Control Class
uacAcc:
  normalClass: 0
  class11: false
  class12: false
  class13: false
  class14: false
  class15: false
 
# Initial PDU sessions to be established
sessions:
  - type: 'IPv4'
    apn: 'voip'
    slice:
      sst: 1
      sd: 0x000002
 
# Configured NSSAI for this UE by HPLMN
configured-nssai:
  - sst: 1
    sd: 0x000002
 
# Default Configured NSSAI for this UE
default-nssai:
  - sst: 1
    sd: 0x000002
 
# Supported integrity algorithms by this UE
integrity:
  IA1: true
  IA2: true
  IA3: true
 
# Supported encryption algorithms by this UE
ciphering:
  EA1: true
  EA2: true
  EA3: true
 
# Integrity protection maximum data rate for user plane
integrityMaxRate:
  uplink: 'full'
  downlink: 'full'
```
 
### Changes in configuration files of UE3 (IMSI-999700000000003)
- To excute the configuration file
  ```bash
  sudo build/nr-ue -c config/open5gs-ue3.yaml
 
  ```
- `UERANSIM/config/open5gs-ue3.yaml`
```bash
# IMSI number of the UE. IMSI = [MCC|MNC|MSISDN] (In total 15 digits)
supi: 'imsi-999700000000003'
# Mobile Country Code value of HPLMN
mcc: '999'
# Mobile Network Code value of HPLMN (2 or 3 digits)
mnc: '70'
# SUCI Protection Scheme : 0 for Null-scheme, 1 for Profile A and 2 for Profile B
protectionScheme: 0
# Home Network Public Key for protecting with SUCI Profile A
homeNetworkPublicKey: '5a8d38864820197c3394b92613b20b91633cbd897119273bf8e4a6f4eec0a650'
# Home Network Public Key ID for protecting with SUCI Profile A
homeNetworkPublicKeyId: 1
# Routing Indicator
routingIndicator: '0000'
 
# Permanent subscription key
key: '465B5CE8B199B49FAA5F0A2EE238A6BC'
# Operator code (OP or OPC) of the UE
op: 'E8ED289DEBA952E4283B54E88E6183CA'
# This value specifies the OP type and it can be either 'OP' or 'OPC'
opType: 'OPC'
# Authentication Management Field (AMF) value
amf: '8000'
# IMEI number of the device. It is used if no SUPI is provided
imei: '356938035643803'
# IMEISV number of the device. It is used if no SUPI and IMEI is provided
imeiSv: '4370816125816151'
 
# List of gNB IP addresses for Radio Link Simulation
gnbSearchList:
  - 192.168.64.5
 
# UAC Access Identities Configuration
uacAic:
  mps: false
  mcs: false
 
# UAC Access Control Class
uacAcc:
  normalClass: 0
  class11: false
  class12: false
  class13: false
  class14: false
  class15: false
 
# Initial PDU sessions to be established
sessions:
  - type: 'IPv4'
    apn: 'internet'
    slice:
      sst: 2
      sd: 0x000001
 
# Configured NSSAI for this UE by HPLMN
configured-nssai:
  - sst: 2
    sd: 0x000001
 
# Default Configured NSSAI for this UE
default-nssai:
  - sst: 2
    sd: 0x000001
 
# Supported integrity algorithms by this UE
integrity:
  IA1: true
  IA2: true
  IA3: true
 
# Supported encryption algorithms by this UE
ciphering:
  EA1: true
  EA2: true
  EA3: true
 
# Integrity protection maximum data rate for user plane
integrityMaxRate:
  uplink: 'full'
  downlink: 'full'
```
 
### Changes in configuration files of UE4 (IMSI-999700000000004)
- To excute the configuration file
  ```bash
  sudo build/nr-ue -c config/open5gs-ue4.yaml
 
  ```
- `UERANSIM/config/open5gs-ue4.yaml`
```bash
# IMSI number of the UE. IMSI = [MCC|MNC|MSISDN] (In total 15 digits)
supi: 'imsi-999700000000004'
# Mobile Country Code value of HPLMN
mcc: '999'
# Mobile Network Code value of HPLMN (2 or 3 digits)
mnc: '70'
# SUCI Protection Scheme : 0 for Null-scheme, 1 for Profile A and 2 for Profile B
protectionScheme: 0
# Home Network Public Key for protecting with SUCI Profile A
homeNetworkPublicKey: '5a8d38864820197c3394b92613b20b91633cbd897119273bf8e4a6f4eec0a650'
# Home Network Public Key ID for protecting with SUCI Profile A
homeNetworkPublicKeyId: 1
# Routing Indicator
routingIndicator: '0000'
 
# Permanent subscription key
key: '465B5CE8B199B49FAA5F0A2EE238A6BC'
# Operator code (OP or OPC) of the UE
op: 'E8ED289DEBA952E4283B54E88E6183CA'
# This value specifies the OP type and it can be either 'OP' or 'OPC'
opType: 'OPC'
# Authentication Management Field (AMF) value
amf: '8000'
# IMEI number of the device. It is used if no SUPI is provided
imei: '356938035643803'
# IMEISV number of the device. It is used if no SUPI and IMEI is provided
imeiSv: '4370816125816151'
 
# List of gNB IP addresses for Radio Link Simulation
gnbSearchList:
  - 192.168.64.66
 
# UAC Access Identities Configuration
uacAic:
  mps: false
  mcs: false
 
# UAC Access Control Class
uacAcc:
  normalClass: 0
  class11: false
  class12: false
  class13: false
  class14: false
  class15: false
 
# Initial PDU sessions to be established
sessions:
  - type: 'IPv4'
    apn: 'internet'
    slice:
      sst: 2
      sd: 0x000002
 
# Configured NSSAI for this UE by HPLMN
configured-nssai:
  - sst: 2
    sd: 0x000002
 
# Default Configured NSSAI for this UE
default-nssai:
  - sst: 2
    sd: 0x000002
 
# Supported integrity algorithms by this UE
integrity:
  IA1: true
  IA2: true
  IA3: true
 
# Supported encryption algorithms by this UE
ciphering:
  EA1: true
  EA2: true
  EA3: true
 
# Integrity protection maximum data rate for user plane
integrityMaxRate:
  uplink: 'full'
  downlink: 'full'
```
 
### Changes in configuration files of UE5 (IMSI-999700000000005)
- To excute the configuration file
  ```bash
  sudo build/nr-ue -c config/open5gs-ue5.yaml
 
  ```
- `UERANSIM/config/open5gs-ue5.yaml`
```bash
# IMSI number of the UE. IMSI = [MCC|MNC|MSISDN] (In total 15 digits)
supi: 'imsi-999700000000005'
# Mobile Country Code value of HPLMN
mcc: '999'
# Mobile Network Code value of HPLMN (2 or 3 digits)
mnc: '70'
# SUCI Protection Scheme : 0 for Null-scheme, 1 for Profile A and 2 for Profile B
protectionScheme: 0
# Home Network Public Key for protecting with SUCI Profile A
homeNetworkPublicKey: '5a8d38864820197c3394b92613b20b91633cbd897119273bf8e4a6f4eec0a650'
# Home Network Public Key ID for protecting with SUCI Profile A
homeNetworkPublicKeyId: 1
# Routing Indicator
routingIndicator: '0000'
 
# Permanent subscription key
key: '465B5CE8B199B49FAA5F0A2EE238A6BC'
# Operator code (OP or OPC) of the UE
op: 'E8ED289DEBA952E4283B54E88E6183CA'
# This value specifies the OP type and it can be either 'OP' or 'OPC'
opType: 'OPC'
# Authentication Management Field (AMF) value
amf: '8000'
# IMEI number of the device. It is used if no SUPI is provided
imei: '356938035643803'
# IMEISV number of the device. It is used if no SUPI and IMEI is provided
imeiSv: '4370816125816151'
 
# List of gNB IP addresses for Radio Link Simulation
gnbSearchList:
  - 192.168.64.67
 
# UAC Access Identities Configuration
uacAic:
  mps: false
  mcs: false
 
# UAC Access Control Class
uacAcc:
  normalClass: 0
  class11: false
  class12: false
  class13: false
  class14: false
  class15: false
 
# Initial PDU sessions to be established
sessions:
  - type: 'IPv4'
    apn: 'internet2'
    slice:
      sst: 2
      sd: 0x000003
 
# Configured NSSAI for this UE by HPLMN
configured-nssai:
  - sst: 2
    sd: 0x000003
 
# Default Configured NSSAI for this UE
default-nssai:
  - sst: 2
    sd: 0x000003
 
# Supported integrity algorithms by this UE
integrity:
  IA1: true
  IA2: true
  IA3: true
 
# Supported encryption algorithms by this UE
ciphering:
  EA1: true
  EA2: true
  EA3: true
 
# Integrity protection maximum data rate for user plane
integrityMaxRate:
  uplink: 'full'
  downlink: 'full'
```
 
 
## To excute all open 5gs C-Plane Configuration
```bash
./install/bin/open5gs-nrfd & ./install/bin/open5gs-scpd & ./install/bin/open5gs-amfd & ./install/bin/open5gs-smfd -c install/etc/open5gs/smf1.yaml & ./install/bin/open5gs-smfd -c install/etc/open5gs/smf2.yaml & ./install/bin/open5gs-smfd -c ./install/etc/open5gs/smf3.yaml & ./install/bin/open5gs-ausfd & ./install/bin/open5gs-udmd & ./install/bin/open5gs-udrd & ./install/bin/open5gs-pcfd & ./install/bin/open5gs-nssfd & ./install/bin/open5gs-bsfd
```
 
## To stop all open 5gs C-Plane Configuration
```bash
killall open5gs-nrfd open5gs-scpd open5gs-amfd open5gs-smfd open5gs-upfd open5gs-ausfd open5gs-udmd open5gs-pcfd open5gs-nssfd open5gs-bsfd open5gs-udrd open5gs-mmed open5gs-sgwcd open5gs-sgwud open5gs-hssd open5gs-pcrfd
```
