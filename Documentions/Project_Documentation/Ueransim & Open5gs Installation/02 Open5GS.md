# Open5gs Setup and Configurations
This comprehensive guide offers a step-by-step walkthrough for compiling and installing Open5GS 
from source on Debian/Ubuntu-based Linux distributions. Please be aware that versions of Ubuntu 16.04 
(xenial) and earlier, as well as Debian 9 (stretch) and earlier, are not supported.
 
## Step 1: Getting MongoDB
 
To install MongoDB, follow these steps:
 
### 1.1 **Import the public key for the package management system:**
   Before installing MongoDB, it's essential to import the public key for the package management system.
   This key is used to verify the authenticity of the MongoDB packages.
   ```bash
   sudo apt update
   sudo apt install gnupg
   curl -fsSL https://pgp.mongodb.com/server-6.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-6.0.gpg --dearmor
   ```
- `sudo apt update` Updates the local package database to ensure that the latest package information is available.
 
- `sudo apt install gnupg:` Installs the GNU Privacy Guard (GPG), a key management tool required for handling cryptographic operations.
 
- `curl -fsSL https://pgp.mongodb.com/server-6.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-6.0.gpg --dearmor` Fetches the MongoDB public key and saves it in the specified GPG format file (`mongodb-server-6.0.gpg`). This key will be used to verify the MongoDB packages during installation.
 
### 1.2 Create the list file for MongoDB:
```csharp
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```
- The `echo` command is used to write the MongoDB repository details to a file.
- The specified URL `https://repo.mongodb.org/apt/ubuntu` is the MongoDB repository.
- `jammy` is the codename for Ubuntu 22.04.
- `mongodb-org/6.0` indicates the version of MongoDB (version 6.0 in this case).
- `multiverse` is the repository component.
- After running the command, the repository configuration will be saved to the file `/etc/apt/sources.list.d/mongodb-org-6.0.list`. This file is used by the system's package manager to locate MongoDB packages.
 
Now we have successfully created the list file for MongoDB on our Ubuntu 22.04 system.
 
### 1.3 Installing MongoDB on Debian/Ubuntu
- **Update Package Information:**
  Ensures that the package manager has the latest information about available packages.
  ```csharp
  sudo apt update
  ```
- **Install MongoDB Packages**
  ```csharp
  sudo apt install -y mongodb-org
  ```
- **Start MongoDB Service:** Initiates the MongoDB service. If the service is not already running, this command starts it.
  ```csharp
  sudo systemctl start mongod
  ```
-  **Enable MongoDB to Start Automatically:** Configures MongoDB to start automatically on system boot, ensuring persistent availability
   ```csharp
   sudo systemctl enable mongod
   ```
This configuration ensures that MongoDB will automatically start whenever the system boots up. Now, MongoDB is installed and running on your Debian/Ubuntu system. You can proceed with configuring and using MongoDB for your applications.
 
## Step 2: Setting up TUN Device
### 2.1 Create a TUN device named ogstun (not persistent after rebooting):
To facilitate communication between Open5GS components, it's essential to set up a TUN device. Follow the steps below to create and configure a TUN device named `ogstun`. Note that this configuration is not persistent after rebooting.
- **Create TUN Device:**
  ```csharp
  sudo ip tuntap add name ogstun mode tun  // command to add a TUN device named ogstun.
  ```
- **Assign IP Addresses:**
  ```csharp
  sudo ip addr add 10.45.0.1/16 dev ogstun
  sudo ip addr add 2001:db8:cafe::1/48 dev ogstun
  ```
  Assigns both IPv4 and IPv6 addresses to the `ogstun` device. In this example, IPv4 address `10.45.0.1` with a subnet mask of `/16` and IPv6 address `2001:db8:cafe::1` with a subnet mask of `/48` are used.
- **Bring up the TUN Device:**
  ```csharp
  sudo ip link set ogstun up
  ```
## Step 3: Building Open5GS
### 3.1 Installing Dependencies for Building Open5GS from Source
```csharp
sudo apt install python3-pip python3-setuptools python3-wheel ninja-build build-essential flex bison git cmake libsctp-dev libgnutls28-dev libgcrypt-dev libssl-dev libidn11-dev libmongoc-dev libbson-dev libyaml-dev libnghttp2-dev libmicrohttpd-dev libcurl4-gnutls-dev libnghttp2-dev libtins-dev libtalloc-dev meson
```
- `python3-pip`, `python3-setuptools`, `python3-wheel:` Python packages required for certain build tools.
- `ninja-build`, `build-essential`, `flex`, `bison`, `git`, `cmake:` Essential build tools and version control system.
- `libsctp-dev`, `libgnutls28-dev`, `libgcrypt-dev`, `libssl-dev`, `libidn11-dev:` Libraries for secure communication protocols.
- `libmongoc-dev`, `libbson-dev:` MongoDB libraries for specific Open5GS functionalities.
- `libyaml-dev`, `libnghttp2-dev`, `libmicrohttpd-dev`, `libcurl4-gnutls-dev`, `libtins-dev`, `libtalloc-dev`, `meson:` Additional libraries and tools necessary for building Open5GS.
### 3.2 **Clone the Open5GS repository:**
```csharp
git clone https://github.com/open5gs/open5gs
```
### 3.3 **Compile with meson:**
- Navigate to the Open5GS directory using the terminal:
  ```csharp
  cd open5gs
  ```
- Configure the build with Meson, specifying the installation prefix
  ```csharp
  meson build --prefix=`pwd`/install      // The --prefix option sets the installation prefix to the install directory within the current Open5GS directory. Adjust this path as needed.
  ```
- Build Open5GS using Ninja:
  ```csharp
  ninja -C build
  ```
  The -C build option directs Ninja to the build directory where the Meson configuration is stored.
### 3.4 **Check the compilation:**
- This below command is designed to test and validate the attachment procedure in the Evolved Packet Core (EPC) component of your project. Ensure that this process completes without errors to guarantee the integrity of the EPC.
  ```csharp
  ./build/tests/attach/attach
  ```
- This below command is specifically tailored for testing and verifying the registration process within the 5G Core component. Executing this command will help confirm that the registration functionality is correctly implemented and operational.
```csharp
./build/tests/registration/registration
```
**Note**: Replace ./build with the actual path to your build directory if it differs.
### 3.5 **Run all test programs:**
- Open your terminal and navigate to the build directory using the following command:
  ```csharp
   cd build
  ```
- Run all test programs using Meson:
  ```csharp
  meson test -v
  ```
Additionally, you can run specific test programs individually. Below are examples of running two test programs:
- Run the "attach" test program:
  ```csharp
  ./build/tests/attach/attach
  ```
- Run the "registration" test program:
  ```csharp
  ./build/tests/registration/registration
  ```
These examples showcase how to execute specific tests within your build. Adjust the paths and test program names based on our project's structure and requirements.[Output files can be found here](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/tree/main/tests/Registration)
### 3.6 **Perform the installation process:**
- After successfully building the project, the next step is to perform the installation. Follow these commands in your terminal:
  ```csharp
  cd build
  ninja install
  cd ../
  ```
- `cd build`: Change the directory to the 'build' directory. This is typically the directory where the project was built.
 
- `ninja install`: Use the Ninja build system to install the compiled binaries and associated files. Ninja is a fast and efficient build system.
 
- `cd ../`: Move back to the previous directory. This step is often done for organization or to return to the project's root directory

## Step 4. Configure Open5GS
### 4.1 Locate the Configuration File:
- Open the amf.yaml file located in the install/etc/open5gs/ directory.
  ```csharp
  nano install/etc/open5gs/amf.yaml
  ```
### 4.2 Set NGAP IP Address:
- Locate the parameter related to the NGAP (Next-Generation Core Network Application Protocol) IP address. It may look similar to:
  ```csharp
  ngap_ip: 127.0.0.1
  ```
Replace 127.0.0.1 with the desired IP address for NGAP.
### 4.3 Set PLMN ID (Public Land Mobile Network Identity):
- Find the parameter for PLMN ID:
  ```csharp
   plmn_id:
   mcc: 001
   mnc: 01
  ```
  Replace 001 with the desired Mobile Country Code (MCC) and 01 with the Mobile Network Code (MNC).
### 4.4 Set TAC (Tracking Area Code):
- Locate the TAC parameter:
  ```csharp
  tac: 1
  ```
  Replace 1 with the desired Tracking Area Code.
### 4.5 Set NSSAI (5G Slice Selection Assistance Information):
- Find the NSSAI parameters:
  ```csharp
  nssai:
   sst: 1
   sd: c1
  ```
  Replace 1 with the Service Slice Template (SST) and c1 with the Slice Differentiator (SD).
### 4.6 Save Changes:
- Save the changes made to the amf.yaml file.
### 4.7 Restart the AMF:
- After modifying the configuration, restart the AMF to apply the changes.
  ```csharp
  sudo systemctl restart open5gs-amfd
  ```
  This ensures that the new configurations take effect.
## Step 5. Building the WebUI of Open5GS
### 5.1 Download and Import Nodesource GPG Key:
- This step involves updating the package list, installing necessary tools (`ca-certificates`, `curl`, `gnupg`), and creating a directory for the GPG key.
- The Nodesource GPG key is downloaded and imported to facilitate the secure installation of Node.js.
  ```csharp
  $ sudo apt update
  $ sudo apt install -y ca-certificates curl gnupg
  $ sudo mkdir -p /etc/apt/keyrings
  $ curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
  ```
### 5.2 Create deb Repository:
- In this step, a Debian (deb) repository is created to fetch the required Node.js version. The repository configuration is saved to `/etc/apt/sources.list.d/nodesource.list`.
- The Node.js major version is set using the `NODE_MAJOR` variable (in this case, it's set to 20).
  ```csharp
  $ NODE_MAJOR=20
  $ echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
  ```
### 5.3 Run Update and Install Node.js:
- Update the package list again and install Node.js using the newly added repository.
  ```csharp
  $ sudo apt update
  $ sudo apt install nodejs -y
  ```
### 5.4 Install Dependencies for WebUI:
- Start the WebUI by running the npm script. This script is named `dev`.
- Optionally, you can customize the server's listening behavior by setting the `HOSTNAME` or `PORT` environment variables.
  ```charp
  $ npm run dev
  ```
- To set a custom hostname:
  ```csharp
  $ HOSTNAME=192.168.0.11 npm run dev
  ```
- To set a custom port:
  ```csharp
  $ PORT=7777 npm run dev
  ```
## Step 6. Register Subscriber Information:
### 6.1 Access the WebUI:
- Open your web browser and go to `http://127.0.0.1:3000`.
- Login using the following credentials:
   ```
    Username: admin
    Password: 1423
   ```
### 6.2 Add Subscriber Information:
- Navigate to the Subscriber Menu.
- Click on the '+' button to add a new subscriber.
- Provide the IMSI, security context (K, OPc, AMF), and APN for the subscriber.
- Click the 'SAVE' button.

**Note**: Subscribers added through this tool instantly register in the Open5GS HSS/UDR without requiring any daemon restart. However, if you use the WebUI to modify a subscriber's profile, you must restart the Open5GS AMF/MME daemon for the changes to take effect.







