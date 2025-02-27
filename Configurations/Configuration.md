# Open5GS and UERANSIM Installation Guide

## Overview

This guide provides step-by-step instructions for setting up a wireless communication system using Open5GS, Open5GS and UERANSIM. These components collectively create a software-defined radio (SDR) environment for running a 5G network. The guide is divided into three main sections:

1. **Open5GS Installation**
   - Install MongoDB packages and Open5GS on recent versions of Ubuntu.
   - Install the Web UI of Open5GS.

   ```bash
    $ curl -fsSL https://pgp.mongodb.com/server-6.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-6.0.gpg --dearmor
    $ echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
    $ sudo apt update
    $ sudo apt install mongodb-org
    $ sudo add-apt-repository ppa:open5gs/latest
    $ sudo apt update
    $ sudo apt install open5gs
    $ sudo apt update
    $ sudo apt install -y ca-certificates curl gnupg
    $ sudo mkdir -p /etc/apt/keyrings
    $ curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
    $ NODE_MAJOR=20
    $ echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
    $ sudo apt update
    $ sudo apt install nodejs -y
    $ curl -fsSL https://open5gs.org/open5gs/assets/webui/install | sudo -E bash -

2. **Configuration & Running**
   - Obtain subscriber information, including MCC/MNC, IMSI, K, and OPc.
   - Connect to http://localhost:3000 using the credentials:
   - Username: admin
   - Password: 12365
   - Navigate to the Subscriber Menu.
   - Click the + button to add a new subscriber.
   - Fill in the IMSI, security context (K, OPc, AMF), and APN of the subscriber.
   - Click the SAVE button.

 3. **Download and Build UERANSIM:**
      ```bash
      cd ~
      git clone https://github.com/aligungr/UERANSIM
      cd UERANSIM
      git checkout 3a96298
 4. **Install UERANSIM**
   To download UERANSIM, open your terminal and run the following commands:
      ```bash
      sudo apt update
      sudo apt upgrade
      sudo apt install make
      sudo apt install g++
      sudo apt install libsctp-dev lksctp-tools
      sudo apt install iproute2
      sudo snap install cmake --classic

 5. **Build UERANSIM**
      ```bash
      cd ~/UERANSIM
      make



