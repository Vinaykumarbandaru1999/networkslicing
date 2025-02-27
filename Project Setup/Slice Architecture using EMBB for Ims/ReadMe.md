# Slice Architecture using EMBB for Ims
![image](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/assets/116576484/b9183944-2e71-49e0-807e-dc369dace82d)


Table of content

2.1. Changes in configuration files of UE1 (IMSI-999700000000006)

2.2. Changes in configuration files of GNB

Changes in configuration files of UERANSIM UE / RAN
3.1. Changes in configuration files of RAN

3.2. Changes in configuration files of AMF

3.3. Changes in configuration files of SMF

3.4. Changes in configuration files of UPF

3.4.1. Running Open5GS

3.4.2. To run gnb and ueransim

3.4.3. To Stop Open5GS


## 3.4.1. Running Open5GS
```diff
./install/bin/open5gs-nrfd & ./install/bin/open5gs-scpd & ./install/bin/open5gs-amfd & ./install/bin/open5gs-smfd &./install/bin/open5gs-upfd & ./install/bin/open5gs-ausfd & ./install/bin/open5gs-udmd & ./install/bin/open5gs-pcfd & ./install/bin/open5gs-nssfd & ./install/bin/open5gs-bsfd & ./install/bin/open5gs-udrd & ./install/bin/open5gs-mmed & ./install/bin/open5gs-sgwcd & ./install/bin/open5gs-sgwud & ./install/bin/open5gs-hssd & ./install/bin/open5gs-pcrfd

```
## 3.4.2. To run gnb and ueransim

```diff
+ sudo build/nr-gnb -c config/open5gs-gnb.yaml
+ sudo build/nr-ue -c config/open5gs-ue.yaml
```
## 3.4.3. To Stop Open5GS
- To stop all Open5GS network functions(NF's)
```diff
+ pkill -f './install/bin/open5gs-'
```
