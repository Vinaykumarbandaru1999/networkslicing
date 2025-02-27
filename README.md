<div align="center">
  <h1>Mobile Computing </h1>
</div>

<div align="center">

#### Master of Engineering in Information Technology  
WS 2023-24

**5G-SA: Open5GS-UERANSIM: Internet, VoIP, Chat and File Sharing**

Submitted by  
Anil Kumar Gadiraju   1428607  
Ankush Laxman Patil   1448072  
Vinay Kumar Bandaru   1447125  
Sahith Kumar Singari   1446809  

Under Guidance - Prof. Dr. Armin Lehmann  

</div>



## Preface

 #### **Instructions to read the README**: 
This README serves as a comprehensive guide providing detailed insights into the implementation of network realization of VoIP, messaging,Internet and file sharing using Open5GS-UERANSIM and other associated components. Readers can conveniently navigate through different sections by simply clicking on the respective links. Certain sections feature step-by-step implementations and some Keynotes denoted by an arrow icon, prompting readers to click on the arrow to view the detailed explanations.

## Important Links
1. [Configuration Files](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/5gtechtribe/Documentations/Config_changes.md)
2. [Project Presentation](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/5gtechtribe/Documentations/Mobile_Computing_project_ppt.pdf)
3. [Log Files](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/tree/main/5gtechtribe/Documentations/Log_Files)
   
 <details>
<summary>Please click on the arrow to test your understanding</summary>
Congratulations! Please take a moment to explore the Table of Contents below. Enjoy your reading journey!
 </details>

# Table of Contents

1. [Introduction](#1-introduction)
2. [Project Architecture](#2-project-architecture)
    - [2.1 Technical Stack](#21-technical-stack)
        - [2.1.1 Linux 22.04](#211-linux-2204)
        - [2.1.2 Open5gs Core](#212-open5gs-core)
        - [2.1.3 UERANSIM](#213-ueransim)
        - [2.1.4 Kamailio SIP Server](#214-kamailio-sip-server)
        - [2.1.5 Linphone](#215-linphone)
        - [2.1.6 NextCloud](#216-nextcloud)
        - [2.1.7 Wireshark](#217-wireshark)
    - [2.2 High-Level Diagram](#22-high-level-diagram)
3. [Design and Implementation](#3-design-and-implementation)
    - [3.1 Setting Up Linux 22.04 for 5G](#31-setting-up-linux-2204-for-5g)
    - [3.2 Open5gs Setup and Configurations](#32-open5gs-setup-and-configurations)
    - [3.3 UERANSIM Setup and Configuration](#33-ueransim-setup-and-configuration)
    - [3.4 Kamailio SIP Server Configurations](#34-kamailio-sip-server-configurations)
    - [3.5 Linphone Configurations](#35-linphone-configurations)
    - [3.6 NextCloud Configuration](#36-nextcloud-configuration)
    - [3.7 Activating the 5G Environment](#37-activating-the-5g-environment)
    - [3.8 Network Slicing](#38-network-slicing)
        - [3.8.1 VoIP Voice Calling](#371-voip-voice-calling)
        - [3.8.2 Messaging](#372-messaging)
        - [3.8.3 Internet](#373-internet)
        - [3.8.4 File Sharing](#374-file-sharing)
4. [Challenges](#4-challenges)
5. [Conclusion](#5-conclusion)
6. [Contribute](#6-contribute)
7. [License](#7-license)
8. [References](#references)


# 1. Introduction

The introduction of 5G technology transformed the landscape of mobile computing, ushering in an era of unprecedented speed, capacity, and connectivity. At the heart of this disruptive ecosystem is the integration of cutting-edge components like the Open5GS Core and UERANSIM RAN, which are critical in unleashing the dynamic possibilities of 5G networks. In our project, we have set out to fully realize the promise of these technologies, allowing for smooth communication among multiple users over various gNBs while exploiting distinct user planes for improved connectivity.

The convergence of Open5GS and UESIM RAN defines our project landscape, which is supplemented by other components such as the Kamailio SIP Server, NextCloud, and Linphone. We hope to build a strong network architecture capable of supporting a wide range of communication services through rigorous installation and configuration. The construction of network slices targeted to specific use cases, such as VoIP voice calling, messaging, internet access, and file sharing, is central to our mission.

In order to accomplish this, we have set up many UPFs and gNBs, each of which serves unique network slices and user planes. We have also integrated multiple network functions (NFs), such as three SMFs (Session Management Functions), to guarantee smooth network connectivity. Our main objective has been to create a robust communication system, thus we have given priority to efficiency, scalability, and dependability throughout the project.

By utilizing parts such as NextCloud, Linphone, and Kamailio Call Server, we can improve our network's performance and enable more sophisticated communication features while maintaining strong security and privacy protocols. Our idea offers a view into the future of telecoms, where new services and seamless connectivity come together to transform communication and interaction in the digital age. It encompasses the spirit of mobile computing.

# 2. Project Architecture
The architecture of the project is designed to harness the capabilities of diverse technologies, carefully orchestrated to achieve efficient and scalable 5G network functionality. Here, we provide insights into the technical stack and present a high-level diagram for better understanding.

## 2.1 Technical Stack

In this section, we will explore the technical components employed in the development of the Open5GS Core and UERANSIM, as well as other relevant elements. Each component is explain below along with download links for easy reference.

### 2.1.1 Linux 22.04
Linux, an open-source operating system kernel, powers a wide range of computing devices, from personal computers to servers and embedded systems. In this project we have used Linux version 22.04 as the operating system to the setup of the 5G infrastructure. Linux 22.04 serves as a reliable foundation for deploying and administering the 5G infrastructure, offering stability and compatibility with essential software and tools required for setting up and managing 5G networks. This version of Linux provided a reliable environment for achieving project objectives, enabling seamless integration and operation of the 5G configuration within defined constraints.[8]

 **Virtualization Software:** Install VirtualBox, which can be downloaded from [VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads). <br>
**Ubuntu ISO:** Download the Ubuntu ISO from the [official Ubuntu website](https://ubuntu.com/download/desktop).

### 2.1.2 Open5gs Core
Open5GS is a robust open-source platform tailored for implementing pivotal aspects of the 5G network architecture. Written in C and designed for Linux-based systems, it facilitates seamless deployment and management of 5G core network elements, supporting dynamic scalability and customization. With distinct functional planes, including the Control Plane and User Plane, Open5GS ensures self-sufficient scaling and dynamic deployments, a cornerstone of Software-Defined Networking (SDN). Key components like UE, UPF, and RAN form the User Plane, while critical functions like SMF and AMF govern the Control Plane. Open5GS empowers the realization of essential network functions, making it a standout choice for deploying 5G Stand-Alone (SA) networks. The image below illustrates the basic architecture of the Open5GS core.

<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\image.png" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 2.1.2 Architecture of Open5gs Core</figcaption>
  </figure>
</div>


**Key Components:**

1. **User Equipment (UE):** Devices used by end-users for communication.
2. **Next Gen Node Basestation (gNB):** Base station responsible for radio communication with UEs.
3. **Access and Mobility Management Function (AMF):**
   - Terminates RAN Control Plane interface (NG2).
   - Handles NAS termination, ciphering, and integrity protection.
   - Manages mobility, lawful intercept, and access authentication.
4. **User Plane Function (UPF):**
   - Manages QoS, packet routing, and forwarding.
   - Enforces policy rules, handles lawful intercept, and supports traffic accounting.
5. **Session Management Control Function (SMF):**
   - Manages sessions, UE IP address allocation, and policy enforcement.
   - Terminates interfaces towards policy control and charging functions.
6. **Data Network (DN):** Services provided by the operator, internet access, or other services.
7. **Authentication Server Function (AUSF):** Performs authentication processes with the UE.
8. **Unified Data Management (UDM):**
   - Stores authentication credentials and subscription information.
9. **Policy Control Function (PCF):** Governs network behavior through policy rules.

You can download the Open5GS core from the official GitHub repository and also check tthe Community Page:
[Open5GS GitHub Repository](https://github.com/open5gs/open5gs)


### 2.1.3 UERANSIM
UERANSIM is an open-source simulator for User Equipment (UE) in 5G networks. It is developed in C++ and Python programming languages. It leverages various libraries and frameworks to simulate the behavior of User Equipment (UE) in 5G networks. It incorporates protocol stacks compliant with 3GPP specifications to emulate the signaling and data transfer protocols used in 5G networks. This includes protocols for radio access, session management, and mobility management. UERANSIM consists of simulation modules that replicate the functionalities of connection establishment, handover procedures, data transmission, and reception. The implementation ensured that the simulation environment closely mimics real-world conditions, including radio channel characteristics, propagation models, interference effects, and network congestion. It enabled emulating UE behavior across diverse network scenarios, facilitating comprehensive testing and validation of 5G network operations. By incorporating UERANSIM, the project ensured meticulous examination of genuine UE interactions, encompassing registration, authentication, and data transfer processes. This deliberate utilization underscored the project's commitment to rigorous testing methodologies and the advancement of 5G network research and development.

You can download UERANSIM from the official GitHub repository: <br>
[UERANSIM GitHub Repository](https://github.com/aligungr/UERANSIM)
### 2.1.4 Kamailio SIP Server
Kamailio is an open-source SIP server and proxy renowned for its robust features in delivering real-time communication services. It provides users with efficient management and routing capabilities for SIP signaling, simplifying network-to-network communication processes. With its scalability and agility, Kamailio serves as an optimal solution for various applications, ranging from carrier-grade services to small office setups. As a crucial component of our project's Linux-based communication infrastructure, Kamailio was implemented to ensure the reliability and effectiveness of SIP-based communication services. Its deployment facilitated the setup of SIP signaling pathways, user authentication, call routing, and load balancing functionalities. The modular architecture of Kamailio allowed for seamless integration with other project components, enabling interoperability and scalability. Thus, Kamailio played a pivotal role in guaranteeing the dependability and performance of our communication network. [9]

You can download the Kamailio SIP Server from the official GitHub repository:
[Kamailio SIP Server](https://github.com/kamailio/kamailio-docs
)


### 2.1.5 Linphone
Linphone, a flexible open-source program which serves as the primary tool for making calls, offering robust features for internet-based video and audio communication. Its functionality enables users to initiate and administer calls swiftly, supported by a user-friendly interface. The choice to include Linphone in this project emphasized the need for reliable call setup on Linux, ensuring smooth communication for project stakeholders. Linphone's compatibility with Linux 22.04 boosts interoperability and shows a commitment to dependable Linux resources. Key components of Linphone include call initiation, audio and video transmission, call management, and user interface customization. Its implementation of the project facilitates efficient communication set-up and management.[10]

You can download Linphone from the official website:
[Linphone Official Website](https://www.linphone.org/)


### 2.1.6 NextCloud
Nextcloud is a cloud storage platform that facilitates the creation and use of file hosting services with functionality like those of its industry competitors, such as Dropbox. Although Nextcloud is open-source and publicly accessible, it does not provide on-premises file storage hosting. Instead, it provides the option of installation on private servers. File sharing, chatting, updating shared documents, and private information management are just a few of the features that meet a wide range of user needs, from home offices to large-scale corporate settings. [7] It also offers a range of improvements via its Nextcloud Hub, which is distinguished by a high-performance file management backend that expedites user alerts and dramatically lowers server load. Improved page loading times and teamwork tools like the Whiteboard tool and Nextcloud Talk's sophisticated messaging features are among these upgrades. Furthermore, Nextcloud Hub integrates upgrades to groupware features, such as better email threading and drag-and-drop capability, which boost team efficiency and facilitate smooth communication processes.

You can download Nextcloud from the official website:
[Nextcloud Official Website](https://nextcloud.com/install/)

### 2.1.7 Wireshark
Wireshark is a network protocol analyzer that allows users to capture and interactively browse the traffic running on a computer network. It lets users inspect hundreds of different protocols and supports live capture and offline analysis. Wireshark is commonly used for network troubleshooting, analysis, software and communication protocol development. Its application in the project's setup highlights the need for a careful understanding of network dynamics and the maintenance of reliability and effectiveness in network operations.

You can download WireShark from its official website. Here's the link to the official WireShark website: [WireShark Official Website](https://www.wireshark.org/)


## 2.2 High-Level Diagram
In this section, we present a high-level diagram offering a comprehensive understanding of the implementation process. The diagram (Figure 1.2) delineates core components and their interconnections within the system architecture.
<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\Image30.jpg" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 2.2 High-Level Diagram</figcaption>
  </figure>
</div>

Table 1: Role and configuration setup
| VM # | SW & Role                         | IP Address   | OS        | Memory (Min) | HDD (Min) |
|------|-----------------------------------|--------------|-----------|--------------|------------|
|  VM5    | Kamailio v5.5.6 for SIP VoIP     | 192.168.64.15| Ubuntu 22.04 |      4GB        |     25GB       |
|  VM2    | NextCloud v24.0.0 for File sharing | 192.168.64.65 | Ubuntu 22.04 |      4GB        |   25GB         |
|  VM5    | Open5GS v2.6.0 5GC C-Plane       | 192.168.64.3 | Ubuntu 22.04 |          4GB    |      25GB      |
|  VM1    | UERANSIM v3.3.0 UE1                | 192.168.64.5 | Ubuntu 22.04 |          4GB    |     25GB       |
|  VM2   | UERANSIM v3.3.0 UE2                | 192.168.64.65 | Ubuntu 22.04 |          4GB    |        25GB    |
|  VM1    | UERANSIM v3.3.0 UE3                | 192.168.64.5 | Ubuntu 22.04 |       4GB       |       25GB     |
|  VM3    | UERANSIM v3.3.0 UE4                | 192.168.64.66 | Ubuntu 22.04 |      4GB        |     25GB       |
|  VM4    | UERANSIM v3.3.0 UE5                | 192.168.64.67 | Ubuntu 22.04 |      4GB        |     25GB       |
|  VM1    | UERANSIM v3.3.0 RAN(gNodeB1)      | 192.168.64.5 | Ubuntu 22.04 |        4GB      |        25GB    |
|  VM2    | UERANSIM v3.3.0 RAN(gNodeB2)      | 192.168.64.65 | Ubuntu 22.04 |        4GB      |       25GB     |
|  VM3    | UERANSIM v3.3.0 RAN(gNodeB3)      | 192.168.64.66 | Ubuntu 22.04 |      4GB        |        25GB    |
|  VM4    | UERANSIM v3.3.0 RAN(gNodeB4)      | 192.168.64.67 | Ubuntu 22.04 |      4GB        |        25GB    |
|  VM6    | Open5GS v2.6.0 5GC U-Plane1       | 192.168.64.4 | Ubuntu 22.04 |       4GB       |         25GB   |
|  VM7    | Open5GS v2.6.0 5GC U-Plane2       | 192.168.64.6 | Ubuntu 22.04 |       4GB       |          25GB  |
|  VM4    | Open5GS v2.6.0 5GC U-Plane3       | 192.168.64.7 | Ubuntu 22.04 |       4GB       |          25GB  |


Table 2: AMF and NSSF configuration
| Network Function | IP Address    | IP Address on SBI | Supported S-NSSAI                                    |
|------------------|---------------|-------------------|-------------------------------------------------------|
| AMF              | 192.168.64.3  | 127.0.0.5         | SST: 1 SD: 000001, SST: 1 SD: 000002, SST: 2 SD: 000001, SST: 2 SD: 000002, SST: 2 SD: 000003 |
| NSSF-SST1-SD1    | 192.168.64.3  | 127.0.0.10        | SST: 1 SD: 000001                                    |
| NSSF-SST1-SD2    | 192.168.64.3  | 127.0.0.10        | SST: 1 SD: 000002                                    |
| NSSF-SST2-SD1    | 192.168.64.3  | 127.0.0.10        | SST: 2 SD: 000001                                    |
| NSSF-SST2-SD2    | 192.168.64.3  | 127.0.0.10        | SST: 2 SD: 000002                                    |
| NSSF-SST2-SD3    | 192.168.64.3  | 127.0.0.10        | SST: 2 SD: 000003                                    |


Table 3 Data networks
| Data Network | S-NSSAI        | TUNnel interface of DN | DNN       | TUNnel interface of UE | U-Plane # |
|--------------|----------------|------------------------|-----------|------------------------|-----------|
| 10.45.0.1/16 | SST:1 SD:0x000001 | ogstun/10.45.0.1     | Voip      | uesimtun0              | U-Plane 1 |
| 10.46.0.1/16 | SST:1 SD:0x000002 | ogstun2/10.46.0.1    | Voip      | uesimtun0              | U-Plane 2 |
| 10.47.0.1/16 | SST:2 SD:0x000001 | ogstun3/10.47.0.1    | Internet  | uesimtun0              | U-Plane 1 |
| 10.47.0.1/16 | SST:2 SD:0x000002 | ogstun4/10.47.0.1    | Internet | Uesimtun0              | U-Plane 3 |
| 10.48.0.1/16 | SST:2 SD:0x000003 | ogstun4/10.48.0.1    | Internet2 | Uesimtun2              | U-Plane 3 |

Table 4: Subscriber Information
| UE Name | IMSI           | DNN       | Supported S-NSSAI  |
|---------|----------------|-----------|--------------------|
| Ue1     | 901700000000001 | voip      | SST: 1 SD: 0x000001 |
| Ue2     | 901700000000002 | voip      | SST: 1 SD: 0x000002 |
| Ue3     | 901700000000003 | Internet  | SST: 2 SD: 0x000001 |
| Ue4     | 901700000000004 | Internet | SST: 2 SD: 0x000002 |
| Ue5     | 901700000000005 | Internet2 | SST: 2 SD: 0x000003 |

# 3. Design and Implementation

This section will give the detail desscription about the of the necessary steps, configurations, and setups to implement network slicing, VoIP, messaging, file sharing, and streaming services using UERANSIM.

## 3.1 Setting Up Linux 22.04 for 5G
To start the project setup, the first and foremost step is to install the Virtual Machine and set up a Linux Ubuntu operating system. Below are the necessary downloads:

**Virtualization Software:** Install VirtualBox, which can be downloaded from [VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads). <br>
**Ubuntu ISO:** Download the Ubuntu ISO from the [official Ubuntu website](https://ubuntu.com/download/desktop).

In general, you can work on this project in Windows or macOS operating systems. Below are the general steps to install the Linux distribution on both operating systems:

## 3.1.1 Creating a Virtual Machine for Ubuntu on Mac using UTM

1. **Open VirtualBox:** Launch VirtualBox and click on "New" to begin setting up a new virtual machine.

2. **Configure Virtual Machine:**
   - Name: Provide a name for your virtual machine, such as "Ubuntu."
   - Type: Choose "Linux".
   - Version: Select "Ubuntu 64".
   - Memory: Allocate at least 2 GB of RAM.
   - Hard Disk: Opt for creating a new virtual hard disk with sufficient space, e.g., 25 GB.

3. **Adjust System Settings:**
   - Go to the "Settings" menu.
   - Navigate to "System" and set "Hard Disk" as the primary boot option.
   - Under "Storage," mount the Ubuntu ISO in the virtual CD/DVD drive.

4. **Start Virtual Machine:**
   - Launch the virtual machine.
   - It will boot from the Ubuntu ISO, initiating the Ubuntu installation process.


<details>
<summary>Alternatively, The Installtion Process for Vindows follow the steps mentioed below,</summary>

## 3.1.2 Creating a Virtual Machine for Ubuntu on Windows using VirtualBox

1. **Open VirtualBox:** Launch VirtualBox and click on "New" to set up a new virtual machine.

2. **Configure Virtual Machine:**
   - Name: Provide a name for your virtual machine, e.g., "Ubuntu."
   - Type: Choose "Linux."
   - Version: Select "Ubuntu."
   - Memory: Allocate at least 2 GB of RAM.
   - Hard Disk: Opt for creating a new virtual hard disk with sufficient space, e.g., 25 GB.

3. **Adjust System Settings:**
   - Go to the "Settings" menu.
   - Navigate to "System" and set "Hard Disk" as the primary boot option.
   - Under "Storage," mount the Ubuntu ISO in the virtual CD/DVD drive.

4. **Start Virtual Machine:**
   - Launch the virtual machine.
   - It will boot from the Ubuntu ISO, initiating the Ubuntu installation process.

</details>



## 3.2 Open5gs Setup and Configurations

This section outlines the installation and configuration process for Open5GS Core on Linux 22.04 which is core coponent for 5G network development. It covers setting up installing dependencies like MongoDB, building Open5GS, and configuring its components. Also, The step-by-step guide is given below.
 
<details>
<summary>Step 1 : Installation of MongoDB</summary>

## Step 1 : Installtion of MongoDB
 
### 1.1 Import the public key for the package management system:
   Before installing MongoDB, it's essential to import the public key for the package management system.
   This key is used to verify the authenticity of the MongoDB packages.
   ```bash
   sudo apt update
   sudo apt install gnupg
   curl -fsSL https://pgp.mongodb.com/server-6.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-6.0.gpg --dearmor
   ```
<details>
<summary>Explanation of Commands</summary>

- `sudo apt update`: Updates the local package database to ensure that the latest package information is available.

- `sudo apt install gnupg`: Installs the GNU Privacy Guard (GPG), a key management tool required for handling cryptographic operations.

- `curl -fsSL https://pgp.mongodb.com/server-6.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-6.0.gpg --dearmor`: Fetches the MongoDB public key and saves it in the specified GPG format file (`mongodb-server-6.0.gpg`). This key will be used to verify the MongoDB packages during installation.

</details>

 
### 1.2 Create the list file for MongoDB:
```csharp
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```
<details>
<summary>Explanation of Commands</summary>

- The `echo` command is used to write the MongoDB repository details to a file.
- The specified URL `https://repo.mongodb.org/apt/ubuntu` is the MongoDB repository.
- `jammy` is the codename for Ubuntu 22.04.
- `mongodb-org/6.0` indicates the version of MongoDB (version 6.0 in this case).
- `multiverse` is the repository component.
- After running the command, the repository configuration will be saved to the file `/etc/apt/sources.list.d/mongodb-org-6.0.list`. This file is used by the system's package manager to locate MongoDB packages.

</details>

 
Now we have successfully created the list file for MongoDB on our Ubuntu 22.04 system.
 
### 1.3 Installing MongoDB on Debian/Ubuntu


The Below configuration ensures that MongoDB will automatically start whenever the system boots up. Now, MongoDB is installed and running on your Debian/Ubuntu system. You can can use the below commands to test the same.


#### Start MongoDB Service
  ```csharp
sudo systemctl start mongod

#### Stop MongoDB Service
  ```csharp
sudo systemctl stop mongod
  ```
#### Restart MongoDB Service
  ```csharp
sudo systemctl restart mongod
  ```
#### Check MongoDB Service Status
  ```csharp
sudo systemctl status mongod
  ```
#### Enable MongoDB Service to Start on Boot
  ```csharp
sudo systemctl enable mongod
  ```
#### Disable MongoDB Service from Starting on Boot
  ```csharp
sudo systemctl disable mongod
  ```
</details>

<details>
<summary> Step 2 : Setting up TUN Device</summary>

## Step 2 : Setting up TUN Device.

### 2.1 Create a TUN device named ogstun (not persistent after rebooting):
To establish communication between Open5GS components, it's essential to set up a TUN device. Follow the steps below to create and configure a TUN device named `ogstun`. Note that this configuration is not persistent after rebooting.

**Create TUN Device:**
  ```csharp
  sudo ip tuntap add name ogstun mode tun  // command to add a TUN device named ogstun.
  ```
**Assign IP Addresses:**
  ```csharp
  sudo ip addr add 10.45.0.1/16 dev ogstun
  sudo ip addr add 2001:db8:cafe::1/48 dev ogstun
  ```
  Assigns both IPv4 and IPv6 addresses to the `ogstun` device. In this example, IPv4 address `10.45.0.1` with a subnet mask of `/16` and IPv6 address `2001:db8:cafe::1` with a subnet mask of `/48` are used.

**Bring up the TUN Device:**
  ```csharp
  sudo ip link set ogstun up
  ```
</details>

<details>
<summary>Step 3 : Building Open5GS</summary>

## Step 3 : Building Open5GS
### 3.1 Installing Dependencies for Building Open5GS from Source
```csharp
sudo apt install python3-pip python3-setuptools python3-wheel ninja-build build-essential flex bison git cmake libsctp-dev libgnutls28-dev libgcrypt-dev libssl-dev libidn11-dev libmongoc-dev libbson-dev libyaml-dev libnghttp2-dev libmicrohttpd-dev libcurl4-gnutls-dev libnghttp2-dev libtins-dev libtalloc-dev meson
```
<details>
<summary>Explanation of Dependencies</summary>

- `python3-pip`, `python3-setuptools`, `python3-wheel`: Python packages required for certain build tools.
- `ninja-build`, `build-essential`, `flex`, `bison`, `git`, `cmake`: Essential build tools and version control system.
- `libsctp-dev`, `libgnutls28-dev`, `libgcrypt-dev`, `libssl-dev`, `libidn11-dev`: Libraries for secure communication protocols.
- `libmongoc-dev`, `libbson-dev`: MongoDB libraries for specific Open5GS functionalities.
- `libyaml-dev`, `libnghttp2-dev`, `libmicrohttpd-dev`, `libcurl4-gnutls-dev`, `libtins-dev`, `libtalloc-dev`, `meson`: Additional libraries and tools necessary for building Open5GS.

</details>

### 3.2 **Clone the Open5GS repository:**
```csharp
git clone https://github.com/open5gs/open5gs
```
### 3.3 **Compile with meson:**
Navigate to the Open5GS directory using the terminal:
  ```csharp
  cd open5gs
  ```
Configure the build with Meson, specifying the installation prefix
  ```csharp
  meson build --prefix=`pwd`/install    
  ```
Build Open5GS using Ninja:
  ```csharp
  ninja -C build
  ```
  The -C build option directs Ninja to the build directory where the Meson configuration is stored.
### 3.4 **Check the compilation:**
This below command is designed to test and validate the attachment procedure in the Evolved Packet Core (EPC) component of your project. Ensure that this process completes without errors to guarantee the integrity of the EPC.
  ```csharp
  ./build/tests/attach/attach
  ```
This below command is specifically tailored for testing and verifying the registration process within the 5G Core component. Executing this command will help confirm that the registration functionality is correctly implemented and operational.
```csharp
./build/tests/registration/registration
```
**Note**: Replace ./build with the actual path to your build directory if it differs.
### 3.5 **Run all test programs:**
Open your terminal and navigate to the build directory using the following command:
  ```csharp
   cd build
  ```3.8 Network Slicing
Run all test programs using Meson:
  ```csharp
  meson test -v
  ```
Additionally, you can run specific test programs individually. Below are examples of running two test programs:
Run the "attach" test program:
  ```csharp
  ./build/tests/attach/attach
  ```
Run the "registration" test program:
  ```csharp
  ./build/tests/registration/registration
  ```
These examples showcase how to execute specific tests within your build. Adjust the paths and test program names based on our project's structure and requirements. [Output files can be found here](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/tree/main/tests/Registration)

### 3.6 **Perform the installation process:**
After successfully building the project, the next step is to perform the installation. Follow these commands in your terminal:
  ```csharp
  cd build
  ninja install
  cd ../
  ```
<details>
<summary>Explanation of Commands</summary>

- `cd build`: Change the directory to the 'build' directory. This is typically the directory where the project was built.
 
- `ninja install`: Use the Ninja build system to install the compiled binaries and associated files. Ninja is a fast and efficient build system.
 
- `cd ../`: Move back to the previous directory. This step is often done for organization or to return to the project's root directory.

</details>
</details>

 <details>
<summary>Step 4 : Configure Open5GS</summary>

## Step 4 : Configure Open5GS
### 4.1 Locate the Configuration File:
Open the amf.yaml file located in the install/etc/open5gs/ directory.
  ```csharp
  nano install/etc/open5gs/amf.yaml
  ```
### 4.2 Set NGAP IP Address:
Locate the parameter related to the NGAP (Next-Generation Core Network Application Protocol) IP address. It may look similar to:
  ```csharp
  ngap_ip: 127.0.0.1
  ```
Replace 127.0.0.1 with the desired IP address for NGAP.
### 4.3 Set PLMN ID (Public Land Mobile Network Identity):
Find the parameter for PLMN ID:
  ```csharp
   plmn_id:
   mcc: 001
   mnc: 01
  ```
  Replace 001 with the desired Mobile Country Code (MCC) and 01 with the Mobile Network Code (MNC).
### 4.4 Set TAC (Tracking Area Code):
Locate the TAC parameter:
  ```csharp
  tac: 1
  ```
  Replace 1 with the desired Tracking Area Code.
### 4.5 Set NSSAI (5G Slice Selection Assistance Information):
Find the NSSAI parameters:
  ```csharp
  nssai:
   sst: 1
   sd: c1
  ```
  Replace 1 with the Service Slice Template (SST) and c1 with the Slice Differentiator (SD).
### 4.6 Save Changes:
Save the changes made to the amf.yaml file.
### 4.7 Restart the AMF:
After modifying the configuration, restart the AMF to apply the changes.
  ```csharp
  sudo systemctl restart open5gs-amfd
  ```
  This ensures that the new configurations take effect.

</details>

 <details>
<summary>Step 5 : Building the WebUI of Open5GS</summary>


## Step 5 : Building the WebUI of Open5GS
### 5.1 Download and Import Nodesource GPG Key:
This step involves updating the package list, installing necessary tools (`ca-certificates`, `curl`, `gnupg`), and creating a directory for the GPG key.
The Nodesource GPG key is downloaded and imported to facilitate the secure installation of Node.js.
  ```csharp
  $ sudo apt update
  $ sudo apt install -y ca-certificates curl gnupg
  $ sudo mkdir -p /etc/apt/keyrings
  $ curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
  ```
### 5.2 Create deb Repository:
In this step, a Debian (deb) repository is created to fetch the required Node.js version. The repository configuration is saved to `/etc/apt/sources.list.d/nodesource.list`.

  ```csharp
  $ NODE_MAJOR=20
  $ echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
  ```
<details>
<summary>Explanation of Environment Variable</summary>

The Node.js major version is set using the `NODE_MAJOR` variable. In this case, it's set to 20.

</details>

### 5.3 Run Update and Install Node.js:
 Update the package list again and install Node.js using the newly added repository.
  ```csharp
  $ sudo apt update
  $ sudo apt install nodejs -y
  ```
### 5.4 Install Dependencies for WebUI:
Start the WebUI by running the npm script. This script is named `dev`.
Optionally, you can customize the server's listening behavior by setting the `HOSTNAME` or `PORT` environment variables.
  ```charp
  $ npm run dev
  ```
To set a custom hostname:
  ```csharp
  $ HOSTNAME=192.168.0.11 npm run dev
  ```
To set a custom port:
  ```csharp
  $ PORT=7777 npm run dev
  ```
  
</details>
<details>
<summary>Step 6 : Register Subscriber Information</summary>

## Step 6 : Register Subscriber Information
### 6.1 Access the WebUI:
Open your web browser and go to `http://127.0.0.1:3000`.
 Login using the following credentials:
   ```
    Username: admin
    Password: 1423
   ```
### 6.2 Add Subscriber Information:
- Navigate to the Subscriber Menu.
- Click on the '+' button to add a new subscriber.
- Provide the IMSI, security context (K, OPc, AMF), and APN for the subscriber.
- Click the 'SAVE' button.

<details>
<summary>Note</summary>

Subscribers added through this tool instantly register in the Open5GS HSS/UDR without requiring any daemon restart. However, if you use the WebUI to modify a subscriber's profile, you must restart the Open5GS AMF/MME daemon for the changes to take effect.

</details>
</details>



## 3.3 UERANSIM Setup and Configuration

This comprehensive guide outlines the steps and commands necessary for installing UERANSIM on an Ubuntu-based system. Each step is explained in detail to ensure a smooth installation process.

### Prerequisites

Before initiating the installation, make sure your system meets the following requirements:

- Ubuntu 16.04 or a later version in general (In this Project we have used 22.04 LTS)
- CMake 3.17 or a later version
- gcc 9.0.0 or a later version
- g++ 9.0.0 or a later version

 <details>
<summary>Step 1 : Clone the UERANSIM Repository
</summary>

## Step 1 : Clone the UERANSIM Repository


To acquire the UERANSIM source code and set up the development environment, follow the steps below:

1. **Navigate to Home Directory:** Open a terminal and change to the home directory using the following command:

   ```bash
   cd ~
</details>
 <details>
<summary>Step 2: Install Dependencies
</summary>

## Step 2: Install Dependencies
Updating System Dependencies
Before proceeding with the installation of UERANSIM, ensure that your system dependencies are up-to-date. Follow these commands to update and upgrade your system:

### 2.1 Update Package Lists


```csharp
sudo apt update
```
This command updates the package lists, ensuring that your system has information about the latest available packages.

Upgrade Installed Packages**

```csharp
sudo apt upgrade
```
This command upgrades the installed packages to their latest versions, ensuring that your system is equipped with the latest security patches and improvements.

Installing UERANSIM Dependencies
To run UERANSIM, you need to install certain dependencies. Use the following commands to install the required tools and libraries:

**Install Essential** 
```csharp

sudo apt install make gcc g++ libsctp-dev lksctp-tools iproute2
```
This command installs essential tools and libraries necessary for compiling and running UERANSIM. The packages include make for building, gcc and g++ for compiling code, libsctp-dev for SCTP protocol support, lksctp-tools for additional SCTP tools, and iproute2 for network configuration.

**Install CMake (Snap)**
```csharp
sudo snap install cmake --classic
```
This command installs CMake using Snap, a package management system. CMake is required for building UERANSIM. The --classic flag allows CMake to access system resources, ensuring compatibility.
</details>

 <details>
<summary>Step 3 : Build UERANSIM</summary>



## Step 3: Build UERANSIM

To compile the UERANSIM source code and generate the necessary executable binaries and dynamic libraries, follow these steps:

### Navigate to the UERANSIM Directory

Open a terminal and change to the UERANSIM directory using the following command:

```csharp
cd ~/UERANSIM
```

This command ensures that you are in the correct directory to build the UERANSIM project.

### Build the Project

Execute the make command to initiate the build process:

```csharp
make
```

The make command orchestrates the compilation of the UERANSIM source code. It handles the compilation process, linking, and other necessary steps to create the executable binaries. The resulting files will be stored in the ~/UERANSIM/build directory.

Now, you have successfully built UERANSIM and can proceed to run the simulator.
</details>

 <details>
<summary>Step 4 : Run UERANSIM</summary>



## Step 4: Run UERANSIM

## Running UERANSIM Executables

Now that you have successfully built UERANSIM, follow these steps to run the main executables and initiate 5G network simulations:

### Navigate to the Build Directory

Change to the UERANSIM build directory using the following command:

```csharp
cd ~/UERANSIM/build
```

This command ensures that you are in the correct directory to execute the UERANSIM main executables.

### Launch gNB (RAN) Executable

Execute the following command to launch the 5G gNB (Radio Access Network) main executable:

```csharp
./nr-gnb
```

This command initiates the 5G gNB, simulating the behavior of a base station in the UERANSIM environment.

### Launch UE (User Equipment) Executable

Execute the following command to launch the 5G UE main executable:

```csharp
./nr-ue
```

This command starts the 5G UE, simulating the behavior of a user device in the UERANSIM environment.

### Note: Optional Components

The nr-binder and libdevbnd.so components are optional and mainly used for binding UE's internet connectivity to an arbitrary application. In typical scenarios, these components are not required.

Now, UERANSIM is running with the gNB and UE components, allowing you to simulate and test 5G network scenarios. 

In conclusion, you have successfully completed the installation and setup of UERANSIM, an open-source 5G UE and gNB simulator. By following steps the provided instructions, you have:

1. Cloned the UERANSIM repository from the official GitHub source.
2. Ensured that your system dependencies are up-to-date and installed the required tools and libraries for UERANSIM.
3. Built the UERANSIM project, generating executable binaries and dynamic libraries.
4. Launched the main executables for 5G gNB (RAN) and UE (User Equipment) in the UERANSIM environment.

With UERANSIM now operational, you can delve into 5G network simulations, test different scenarios, and explore the capabilities of your virtualized 5G environment.


# Data Plane Usage with UERANSIM

## Overview
UERANSIM introduces a TUN interface to leverage the internet connectivity of the UE. From version v2.2.1 onwards, the TUN interface settings are automatically configured.

## TUN Interface Setup
Each PDU session initiates a TUN interface. Upon successful PDU session setup, the UE executes these tasks automatically:
- Creation of a TUN interface.
- Configuration of a routing table, IP rule, and IP route.

> **Note:** Be cautious as the routing setups might interfere with your existing network configurations. To bypass automatic routing setups, launch the UE with `nr-ue --no-route-config`. However, the creation of the TUN interface post-PDU session is mandatory.

> **Caution:** Running the UE and Core Network on the same system can lead to issues. It is advisable to use separate systems for UERANSIM and the core network, which can be either physical or virtual machines.

## Utilizing the TUN Interface
To manually engage with the interface, direct your TCP/IP socket to the `uesimtunX` interface. Examples include:
- `ping -I uesimtun0 google.com`
- `sudo curl --interface uesimtun0 google.com`

Additionally, we offer the experimental `./nr-binder` tool for easy connection utilization.

## Using TUN with `./nr-binder`
The `./nr-binder` tool allows you to bind the `uesimtunX` interface to various applications.

> **Note:** Ensure automatic routing setups are active when using `./nr-binder` (i.e., do not initiate the UE with `--no-routing-config`).

> **Warning:** The `./nr-binder` tool is in the experimental phase and may not work with certain applications.

### Usage
```csharp

./nr-binder {PDU-SESSION-IP-ADDRESS} {COMMAND} {ARGS}

```

For instance: ' ./nr-binder 10.45.0.2 curl google.com '

This command enables the curl command to use the UE's internet connection through the IP 10.45.0.2.

You can also bind web browsers, like Firefox: './nr-binder 10.45.0.2 firefox'
> **Reminder:** Terminate all Firefox processes before executing the above command.

## Troubleshooting
If you face internet connectivity issues, ensure the following:
- UERANSIM and the core network are correctly configured.
- A PDU Session is established successfully.
- The IP address in `nr-binder` matches the PDU Session's IP.

> **Note:** The routing configurations in UERANSIM are experimental and not the main feature. It's recommended to bind applications directly to the TUN interface for reliable UE internet connectivity.


</details>

## 3.4 Kamailio SIP Server Configurations
This guide provides instructions for establishing a SIP proxy using Kamailio on an Ubuntu 22.04 server. SIP, or Session Initiation Protocol, serves as the foundation for contemporary VoIP communication, facilitating smooth interactions encompassing voice and video calls, messaging, and various digital exchanges. 

<details>
<summary>Step 1 : Installing Kamailio</summary>

## Step 1: Installing Kamailio
To begin, update your system's package list:

```bash
sudo apt-get update
```
Then, install Kamailio and the required SIP modules:

```bash
sudo apt-get install kamailio kamailio-sqlite-modules kamailio-tls-modules
```
</details>

<details>
<summary>Step 2 : Configuring Kamailio</summary>

## Step 2: Configuring Kamailio
Edit the Kamailio configuration file located at /etc/kamailio/kamailio.cfg using your preferred text editor. You'll need to set several parameters to configure Kamailio as a SIP proxy:

```bash
nano /etc/kamailio/kamailio.cfg
```

Within the configuration file, set the SIP domain and listening interfaces. Look for the #!define WITH_MYSQL directive and uncomment it if you are using MySQL as your database backend. Similarly, uncomment the #!define WITH_TLS if you plan to use TLS for secure SIP communication.
</details>
<details>
<summary>Step 3 : Creating the SIP User Database</summary>


## Step 3: Creating the SIP User Database
To enable Kamailio to manage users, you'll need to create a database. You can use SQLite, as specified during the installation, or any other supported database system. Here, we'll create a simple SQLite database:

```bash
kamdbctl create
```

Follow the prompts to set up the database. Once created, add users to the database using Kamailio's user management tool:
</details>

<details>
<summary>Step 4 : Starting Kamailio</summary>

## Step 4: Starting Kamailio
After completing the configuration, start the Kamailio service:

```bash
sudo systemctl start kamailio
```

Ensure Kamailio starts automatically on boot:

```bash
sudo systemctl enable kamailio
```

Verify the status of the Kamailio service to ensure it's running properly:

```bash
sudo systemctl status kamailio
```
</details>

<details>
<summary>Step 5 : Testing the Configuration</summary>


## Step 5 : Testing the Configuration
To confirm that Kamailio is functioning correctly, use a SIP client to register with the server using the user credentials created earlier. Successful registration and call tests will confirm that Kamailio is properly set up as a SIP proxy.


</details>


## 3.5 Linphone Configurations

<details>
<summary>Step 1 : Installation on Linux (Ubuntu)</summary>

## Installation on Linux (Ubuntu)

### Update Package Lists

Before installing Linphone, update your package lists to access the latest versions of available software:

```bash
sudo apt-get update
```

### Install Linphone

Install Linphone from the default repositories:

```bash
sudo apt-get install linphone -y
```
</details>
<details>
<summary>Step 2 : Configuration</summary>

## Configuration

After installing Linphone, configure it by setting up a SIP account to start making or receiving calls.

### Launch Linphone

Start Linphone from the applications menu or by executing `linphone` in the terminal.

### Set Up a SIP Account

Upon opening Linphone for the first time, you may be prompted to set up a SIP account. You can create a new account with Linphone or use an existing one. Enter your SIP username, password, and the server domain.

### Configure Audio and Video Settings

Adjust audio and video settings under **Settings** > **Preferences** in the Linphone application, including selecting preferred devices and codecs.

### Making and Receiving Calls

Make calls by entering the SIP address of the contact and pressing the call button. Linphone automatically notifies you of incoming calls when running.

</details>

## 3.6 NextCloud Configuration
Nextcloud is a file sharing server that permits you to store your personal content, like documents and pictures, in a centralized location, much like Dropbox. The difference with Nextcloud is that all of its features are open-source. It also returns the control and security of your sensitive data back to you, thus eliminating the use of a third-party cloud hosting service.

<details>
<summary>Step 1 :  Installing Nextcloud</summary>

## Step 1 :  Installing Nextcloud
We will be installing Nextcloud using the Snap packaging system. This packaging system, available on Ubuntu 22.04 by default, allows organizations to ship software, along with all associated dependencies and configuration, in a self-contained unit with automatic updates. This means that instead of installing and configuring a web and database server and then configuring the Nextcloud app to run on it, we can install the snap package which handles the underlying systems automatically.

- Download the Nextcloud snap package and install it on the system, type:
  ```bash
  sudo snap install nextcloud
  ```
- The Nextcloud package will be downloaded and installed on your server. You can confirm that the installation process was successful by listing the changes associated with the snap:
  ```bash
  snap changes nextcloud
  ```
</details>

<details>
<summary>Step 2 : Configuring an Administrative Account</summary>

## Step 2: Configuring an Administrative Account
To configure Nextcloud with a new administrator account, use the nextcloud.manual-install command. You must pass in a `username` and a `password` as arguments:
```bash
sudo nextcloud.manual-install sammy password
```
</details>

<details>
<summary>Step 3 : Adjusting the Trusted Domains</summary>

## Step 3: Adjusting the Trusted Domains
- You can view the current settings by querying the value of the trusted_domains array:
  ```bash
  sudo nextcloud.occ config:system:get trusted_domains
  ```
- Currently, only `localhost` is present as the first value in the array. We can add an entry for our server’s domain name or IP address by typing:
  ```bash
  sudo nextcloud.occ config:system:set trusted_domains 1 --value=example.com
  ```
- If we query the trusted domains again, we will see that we now have two entries:
  ```bash
  sudo nextcloud.occ config:system:get trusted_domains
  ```
</details>

<details>
<summary>Step 4 : Securing the Nextcloud Web Interface with SSL</summary>

## Step 4: Securing the Nextcloud Web Interface with SSL

- Start by opening the ports in the firewall that Let’s Encrypt uses to validate domain ownership. This will make your Nextcloud login page publicly accessible, but since we already have an administrator account configured, no one will be able to hijack the installation:
  ```bash
  sudo ufw allow 80,443/tcp
  ```
- Next, request a Let’s Encrypt certificate by typing:
  ```bash
  sudo nextcloud.enable-https lets-encrypt
  ```
</details>

<details>
<summary>Step 5 : Logging in to the Nextcloud Web Interface</summary>

## Step 5: Logging in to the Nextcloud Web Interface
Now that Nextcloud is configured, visit your server’s domain name or IP address in your web browser:
```
https://example.com
```
Since you have already configure an administrator account from the command line, you will be taken to the Nextcloud login page. Enter the credentials you created for the administrative user:

Click the Log in button to log in to the Nextcloud web interface.</details>

## 3.7 Activating the 5G Environment

After the installation of all components and setting up the environment, activation of the components based on the slice is necessary. The following steps outline the general process we use to activate the environment, along with the corresponding commands:

1. Start Open5GS Core Components:

Use the following commands to start the Open5GS core components:
  ```csharp
sudo service open5gs-nrfd restart
sudo service open5gs-amfd restart
sudo service open5gs-smfd restart
  ```
2. Check Component Status:
After starting the core components, verify their status using the following commands:
  ```csharp
sudo service open5gs-amfd status
sudo service open5gs-smfd status
  ```

3. Restart NSSF Config Files:

Restart the newly created NSSF config files for each SST/SD combination, and stop the default file nssf.yaml. Use commands similar to:
  ```csharp
sudo service open5gs-nssfd-sst1-sd1 restart
sudo service open5gs-nssfd-sst1-sd1 status
  ```

4. Start Open5GS U-Plane Components:
Execute the following commands to start Open5GS U-Plane components:

  ```csharp
sudo service open5gs-upfd restart
sudo service open5gs-upfd status
  ```
5. Run UERANSIM (gNodeB):
Execute UERANSIM (gNodeB) using the command:

  ```csharp
cd /UERANSIM/config
../build/nr-gnb -c open5gs-gnb.yaml
  ```

6. Attach UEs:

Register the UERANSIM UEs with the 5GC and establish PDU sessions. Use commands similar to:

  ```csharp
sudo ./build/nr-ue -c open5gs-ue-sst1-sd1.yaml
  ```

7. Verify PDU Session Establishment:
After successful PDU session establishment, verify the IP address assigned to the TUN interface and check relevant logs for confirmation.

8. Access Services using Network Slices:
Once PDU sessions for all UEs are established, access services using the defined network slices of VoIP, Messgaing,Internet and Filesharing

## 3.8 Network Slicing
In this section, we will delve into the four major functionalities achieved through different slicing techniques:

1. **VoIP (Voice over Internet Protocol):** Utilizing SIP (Session Initiation Protocol) for establishing voice calls over the Internet.
2. **Messaging:** Enabling text-based communication between users over the network.
3. **Internet:** Providing access to web services and online resources through the network.
4. **File Sharing:** Facilitating the exchange of files and documents between users via the network.

## 3.8.1 VoIP Voice Calling

### Network Slice Configuration for VoIP

#### Components Configured:
- **Kamailio Server:** Configured to facilitate VoIP communication.
- **Linphone VoIP Client:** Installed and configured for SIP VoIP Calling.
- **User Equipment (UE) 1 and UE 2:** Configured to communicate with each other via VoIP.


#### VoIP Call Setup:

1. **UE IP Address Assignment:**
   - IP addresses assigned on the 'uesimtun0' interface.

2. **Accessing VoIP Calling Service:**
   - Utilized 'nr-binder' tool from UERANSIM:
     - For UE1: `sh nr-binder 10.47.0.3 /path/to/Linphone`
     - For UE2: `sh nr-binder 10.48.0.2 /path/to/Linphone`

3. **Linphone Configuration:**
   - Subscriber accounts registered in Kamailio database logged in on both UEs.
   - VoIP call initiated by dialing 'ue_sst_sd1' from UE2 to UE1.

<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\Image1.jpg" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 3.7.1.3  Activation of both user to establish communication</figcaption>
  </figure>
</div>

1. **VoIP Call Process:**
   - **Initiation:**
     - User 1 initiates VoIP call.
     - Ringing notification appears on User 2's interface.
<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\Image11.jpg" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 2.1.2  Linphone Interface of UE2 Receivesthe Call from UE1 </figcaption>
  </figure>
</div>

<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\Image2.jpg" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 2.1.2 VoIP Call Initiation </figcaption>
  </figure>
</div>

   - **Acceptance:**
     - Upon acceptance by User 2, the session is established between both users.

<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\Image3.jpg" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 2.1.2 VoIP Voice call Acceptance from UE2</figcaption>
  </figure>
</div>


#### Wireshark Analysis:

- **Session Request:**
  - Initiation of ringing.
  - Capture of SIP proxy URI.
  - Utilization of SIP/SDP protocol.

<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\image-4.png" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 2.1.2 Wireshark Capture on UE1 for Network Slice for VOIP Voice Calls</figcaption>
  </figure>
</div>
<details>
  <summary> Wireshark Capture at UE1 </summary>

  
  Frame 580: 1182 bytes on wire (9456 bits), 1182 bytes captured (9456 bits) on interface any, id 0
  Linux cooked capture v1
  Internet Protocol Version 4, Src: 192.168.64.5, Dst: 192.168.64.15
  User Datagram Protocol, Src Port: 5060, Dst Port: 5060
  Session Initiation Protocol (INVITE)
      Request-Line: INVITE sip:user2@192.168.64.15 SIP/2.0
          Method: INVITE
          Request-URI: sip:user2@192.168.64.15
          [Resent Packet: False]
      Message Header
          Via: SIP/2.0/UDP 192.168.64.5:5060;branch=z9hG4bK.EJg6~1okh;rport
          From: "user1" <sip:user1@192.168.64.15>;tag=u~VcKCvDH
          To: sip:user2@192.168.64.15
          CSeq: 20 INVITE
          Call-ID: YngmydNzcJ
          [Generated Call-ID: YngmydNzcJ]
          Max-Forwards: 70
          Supported: replaces, outbound, gruu
          Allow: INVITE, ACK, CANCEL, OPTIONS, BYE, REFER, NOTIFY, MESSAGE, SUBSCRIBE, INFO, PRACK, UPDATE
          Content-Type: application/sdp
          Content-Length: 493
          Contact: <sip:user1@192.168.64.5;transport=udp>;expires=3600;+sip.instance="<urn:uuid:86046623-b315-00d5-aeb8-2b2effff4750>"
          User-Agent: Linphone Desktop/ (Ubuntu 22.04.3 LTS, Qt 5.15.3) LinphoneCore/4.4.21
      Message Body
          Session Description Protocol
              Session Description Protocol Version (v): 0
              Owner/Creator, Session Id (o): user1 1709 346 IN IP4 192.168.64.5
              Session Name (s): Talk
              Connection Information (c): IN IP4 192.168.64.5
              Time Description, active time (t): 0 0
              Session Attribute (a): rtcp-xr:rcvr-rtt=all:10000 stat-summary=loss,dup,jitt,TTL voip-metrics
              Media Description, name and address (m): audio 7078 RTP/AVP 96 97 98 0 8 101 99 100
              Media Attribute (a): rtpmap:96 opus/48000/2
              Media Attribute (a): fmtp:96 useinbandfec=1
              Media Attribute (a): rtpmap:97 speex/16000
              Media Attribute (a): fmtp:97 vbr=on
              Media Attribute (a): rtpmap:98 speex/8000
              Media Attribute (a): fmtp:98 vbr=on
              Media Attribute (a): rtpmap:101 telephone-event/48000
              Media Attribute (a): rtpmap:99 telephone-event/16000
              Media Attribute (a): rtpmap:100 telephone-event/8000

          From: "user1" <sip:user1@192.168.64.15>;tag=u~VcKCvDH
          To: <sip:user2@192.168.64.15>;tag=AeMHZWf
          Call-ID: YngmydNzcJ
  

</details>


- **Upon Call Acceptance:**
  - Establishment of session.
  - Detection of voice channel establishment.

<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\image-3.png" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 2.1.2 Wireshark Capture on UE2 for Network Slice for VOIP Voice Calls</figcaption>
  </figure>
</div>
<details>
  <summary>Wireshark Capture at UE2</summary>

  
  Frame 421: 1309 bytes on wire (10472 bits), 1309 bytes captured (10472 bits) on interface any, id 0
  Linux cooked capture v1
  Internet Protocol Version 4, Src: 192.168.64.65, Dst: 192.168.64.15
  User Datagram Protocol, Src Port: 5060, Dst Port: 5060
  Session Initiation Protocol (200)
      Status-Line: SIP/2.0 200 Ok
          Status-Code: 200
          [Resent Packet: False]
          [Request Frame: 271]
          [Response Time (ms): 10926]
      Message Header
          Via: SIP/2.0/UDP 192.168.64.15;branch=z9hG4bK96e6.a7f8c969c412cce0dae38f9d7e275abd.0
          Via: SIP/2.0/UDP 192.168.64.5:5060;received=192.168.64.5;branch=z9hG4bK.EJg6~1okh;rport=5060
          From: "user1" <sip:user1@192.168.64.15>;tag=u~VcKCvDH
          To: <sip:user2@192.168.64.15>;tag=AeMHZWf
          Call-ID: YngmydNzcJ
          [Generated Call-ID: YngmydNzcJ]
          CSeq: 20 INVITE
          User-Agent: Linphone Desktop/ (Ubuntu 22.04.3 LTS, Qt 5.15.3) LinphoneCore/4.4.21
          Supported: replaces, outbound, gruu
          Allow: INVITE, ACK, CANCEL, OPTIONS, BYE, REFER, NOTIFY, MESSAGE, SUBSCRIBE, INFO, PRACK, UPDATE
          Contact: <sip:user2@192.168.64.65;transport=udp>;expires=3600;+sip.instance="<urn:uuid:86046623-b315-00d5-aeb8-2b2effff4750>"
          Content-Type: application/sdp
          Content-Length: 496
          Record-route: <sip:192.168.64.15;lr>
      Message Body

              Media Attribute (a): rtcp-fb:* trr-int 1000
              Media Attribute (a): rtcp-fb:* ccm tmmbr
              [Generated Call-ID: YngmydNzcJ]
  

</details>

#### Verdict:
The configured network slice enables successful VoIP communication between users on UE1 and UE2 using Linphone to access the Kamailio server.




## 3.8.2 Messaging
In the next scenario, we conducted a test to enable communication between two users using text messages. For this test, we utilized UE1 and UE2. The text message session was initiated from UE1 to UE2. UE2 received the "Hi" message from UE1 and promptly responded. The conversation flow is illustrated in Figure 3.8.2.1 and Figure 3.8.2.2.
<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\Image4.jpg" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 3.8.2.1 UE1 Message Interface of Network message slice </figcaption>
  </figure>
</div>

<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\Image5.jpg" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 3.8.2.2 UE2 Message Interface of Network message slice </figcaption>
  </figure>
</div>


#### Wireshark Analysis:

To analyze the messaging session results, we examined Wireshark logs captured on both UE1 and UE2 devices. Here's what we observed:

- **UE1 Session Initiation Request:**
  - From UE1, we captured the session initiation request, with the message's plain text content visible in its description.

- **UE1 Outbound Message to UE2:**
  - UE1 sent a "Hi User2" message to UE2, detected in the message body of the session initiation protocol. This message was outbound, with a content type of text/plain. (Refer to Figure 1)
<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\image-7.png" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 3.8.2.3 Wireshark capture at UE1 for Network Message Slice </figcaption>
  </figure>
</div>

<details>
  <summary>Wireshark Capture at UE1</summary>

  
  Frame 421: 1309 bytes on wire (10472 bits), 1309 bytes captured (10472 bits) on interface any, id 0
  Linux cooked capture v1
  Internet Protocol Version 4, Src: 192.168.64.65, Dst: 192.168.64.15
  User Datagram Protocol, Src Port: 5060, Dst Port: 5060
  Session Initiation Protocol (200)
      Status-Line: SIP/2.0 200 Ok
          Status-Code: 200
          [Resent Packet: False]
          [Request Frame: 271]
          [Response Time (ms): 10926]
      Message Header
          Via: SIP/2.0/UDP 192.168.64.15;branch=z9hG4bK96e6.a7f8c969c412cce0dae38f9d7e275abd.0
          Via: SIP/2.0/UDP 192.168.64.5:5060;received=192.168.64.5;branch=z9hG4bK.EJg6~1okh;rport=5060
          From: "user1" <sip:user1@192.168.64.15>;tag=u~VcKCvDH
          To: <sip:user2@192.168.64.15>;tag=AeMHZWf
          Call-ID: YngmydNzcJ
          [Generated Call-ID: YngmydNzcJ]
          CSeq: 20 INVITE
          User-Agent: Linphone Desktop/ (Ubuntu 22.04.3 LTS, Qt 5.15.3) LinphoneCore/4.4.21
          Supported: replaces, outbound, gruu
          Allow: INVITE, ACK, CANCEL, OPTIONS, BYE, REFER, NOTIFY, MESSAGE, SUBSCRIBE, INFO, PRACK, UPDATE
          Contact: <sip:user2@192.168.64.65;transport=udp>;expires=3600;+sip.instance="<urn:uuid:86046623-b315-00d5-aeb8-2b2effff4750>"
          Content-Type: application/sdp
          Content-Length: 496
          Record-route: <sip:192.168.64.15;lr>
      Message Body

              Media Attribute (a): rtcp-fb:* trr-int 1000
              Media Attribute (a): rtcp-fb:* ccm tmmbr
              [Generated Call-ID: YngmydNzcJ]
  

</details>

- **UE2 Response:**
  - UE2 responded with a 200 OK message, confirming the reception of the message from UE1. Additionally, UE2 also sent a "Hi User1" message in response. (Refer to Figure 2)

<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\image-9.png" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 3.8.2.4 Wireshark capture at UE2 </figcaption>
  </figure>
</div>

<details>
  <summary>Wireshark Capture for UE2</summary>

  
  Frame 370: 625 bytes on wire (5000 bits), 625 bytes captured (5000 bits) on interface any, id 0
  Linux cooked capture v1
  Internet Protocol Version 4, Src: 192.168.64.15, Dst: 192.168.64.5
  User Datagram Protocol, Src Port: 5060, Dst Port: 5060
  Session Initiation Protocol (MESSAGE)
      Request-Line: MESSAGE sip:user1@192.168.64.5;transport=udp SIP/2.0
          Method: MESSAGE
          Request-URI: sip:user1@192.168.64.5;transport=udp
          [Resent Packet: False]
      Message Header
          Via: SIP/2.0/UDP 192.168.64.15;branch=z9hG4bK65d8.d2060758aa6e88f636f3f1121ca3158e.0
          Via: SIP/2.0/UDP 192.168.64.65:5060;received=192.168.64.65;branch=z9hG4bK.snNto7L18;rport=5060
          From: <sip:user2@192.168.64.15>;tag=1VN2h39V3
          To: sip:user1@192.168.64.15
          CSeq: 20 MESSAGE
          Call-ID: GRn0LvCVMz
          [Generated Call-ID: GRn0LvCVMz]
          Max-Forwards: 69
          Supported: replaces, outbound, gruu
          Date: Tue, 20 Feb 2024 12:50:17 GMT
          Content-Type: text/plain
          Content-Length: 8
          User-Agent: Linphone Desktop/ (Ubuntu 22.04.3 LTS, Qt 5.15.3) LinphoneCore/4.4.21
      Message Body
          Line-based text data: text/plain (1 lines)
              Hi User1
  

</details>

#### Verdict:
The configured network slice facilitates seamless messaging communication between users on UE1 and UE2, utilizing a messaging application to connect to the messaging server.

## 3.8.3 Internet
In this slice configuration, we aimed to enable internet access on UE3. The slice was configured to allow users to open a browser and request data from any domain. To demonstrate this functionality, we utilized the curl command to request the Frankfurt University of Applied Sciences website. The request was successfully retrieved, as depicted in Figure 3.8.3 below.
<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\Image6.jpg" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 3.8.3 Request to fra-uas website through curl command from UE3</figcaption>
  </figure>
</div>


### Wireshark Analysis

To analyze the results, we captured Wireshark logs on UE3. From Figure 3.8.4, the following findings can be drawn:

- DNS request and response messages were captured.
- The requested domain of "Frankfurt University of Applied Sciences" was observed in the DNS request query.
- The UDP protocol was used for DNS query/response.
- The well-defined DNS port 53 was observed in the destination address.
<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\image-8.png" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 3.8.4  Wireshark Capture on UE3 for Network Internet Slice</figcaption>
  </figure>
</div>

<details>
  <summary>Wireshark Capture at UE3</summary>

  
  Frame 588: 100 bytes on wire (800 bits), 100 bytes captured (800 bits) on interface any, id 0
  Linux cooked capture v1
  Internet Protocol Version 4, Src: 192.168.64.5, Dst: 8.8.8.8
      0100 .... = Version: 4
      .... 0101 = Header Length: 20 bytes (5)
      Differentiated Services Field: 0x00 (DSCP: CS0, ECN: Not-ECT)
      Total Length: 84
      Identification: 0x6377 (25463)
      000. .... = Flags: 0x0
      ...0 0000 0000 0000 = Fragment Offset: 0
      Time to Live: 64
      Protocol: UDP (17)
      Header Checksum: 0x0665 [validation disabled]
      [Header checksum status: Unverified]
      Source Address: 192.168.64.5
      Destination Address: 8.8.8.8
  User Datagram Protocol, Src Port: 43011, Dst Port: 53
      Source Port: 43011
      Destination Port: 53
      Length: 64
      Checksum: 0x110f [unverified]
      [Checksum Status: Unverified]
      [Stream index: 9]
      [Timestamps]
      UDP payload (56 bytes)
  Domain Name System (query)
      Transaction ID: 0x38f2
      Flags: 0x0100 Standard query
      Questions: 1
      Answer RRs: 0
      Authority RRs: 0
      Additional RRs: 1
      Queries
          his.frankfurt-university.de: type A, class IN
      Additional records
          <Root>: type OPT
      [Response In: 592]
  

</details>

Accesing the Multiple Web
<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\Image22.jpg" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 3.8.5 web access on UE3 </figcaption>
  </figure>
</div>

<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\image-10.png" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 3.8.6  Wireshark capture of web access on UE3</figcaption>
  </figure>
</div>

#### Verdict:
With the configured network slice, UE3 successfully accesses the internet and retrieves the relevant data.


## 3.8.4 File Sharing
In this section, we configured file transfer between UE4 and UE5 using Nextcloud. Both user and admin configurations were set up, as illustrated in Figure 3.8.4.
<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\Image25.jpg" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 3.8.4 Next cloud interface forsetting up UE4 and UE5 for file transfer communication</figcaption>
  </figure>
</div>


The process of file transfer begins with the establishment of a connection between UE4 and UE5. Subsequently, UE4 initiates the transfer by sending a PDF document file to UE5, as observed in Figure 3.8.5. Once the transfer is completed, Figure 3.8.6 demonstrates that the file has been successfully received on the recipient device.
<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\Image27.jpg" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 3.8.5 UE4 interface on Next Cloud</figcaption>
  </figure>
</div>

<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\Image26.jpg" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 3.8.6 UE5 interface on Next Cloud</figcaption>
  </figure>
</div>


To analyze this file transfer from UE4 to UE5, we captured Wireshark details on both devices. The output of this analysis is shown in Figure Figure 3.8.7 and Figure 3.8.8, respectively.

<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\Image28.jpg" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 3.8.7 Wireshark Capture at UE4 </figcaption>
  </figure>
</div>

<div style="text-align: center;">
  <figure>
    <img src="5gtechtribe\Documentations\Images\Image29.jpg" alt="ITest" style="width: 800px; border: 2px solid black;">
    <figcaption style="color: Gray;">Figure 3.8.8 Wireshark Capture at UE5</figcaption>
  </figure>
</div>
#### Verdict:
The File Sharing slice has been successfully established between UE4 and UE5, allowing seamless file sharing between the users through Nextcloud.

# 4. Challenges
During the implementation of network slicing with Open5GS and UERANSIM, we encountered several challenges that required careful consideration and problem-solving. One significant challenge was ensuring compatibility and interoperability between different components and software versions. Integrating Kamailio server, Linphone, Nextcloud, and other tools required lot of testing, configuration and troubleshooting to address compatibility issues and ensure seamless communication between network elements.

# 5. Conclusion
In this project, we have successfully implemented and evaluated network slicing functionalities using Open5GS and UERANSIM. By configuring different slices for VoIP calling, messaging, internet access, and file sharing, we aimed to showcase the versatility and effectiveness of network slicing in meeting diverse communication requirements. Through meticulous configuration of Kamailio server, Linphone, Nextcloud, and other components, we established seamless communication channels between users, allowing for voice calls, text messaging, internet browsing, and file transfers. Our thorough testing and analysis, including Wireshark packet captures, validated the proper setup and functioning of each network slice, confirming the reliability and scalability of the deployed solutions.

# 6. Contribute
We welcome contributions from everyone! If you'd like to contribute to our project, please follow these steps:

1. Fork the repository and clone it to your local machine.
2. Create a new branch for your changes: `git checkout -b feature/new-feature`.
3. Make your changes and commit them: `git commit -m 'Add new feature'`.
4. Push your changes to your fork: `git push origin feature/new-feature`.
5. Create a pull request (PR) from your fork's branch to our main branch.
6. Ensure that your PR description clearly describes the changes you've made and any issues they address.
7. If needed, feel free to contact any one of our group members via GitHub or LinkedIn for assistance or feedback.

We appreciate your help in making our project better!

# 7. License


# 8. References






























