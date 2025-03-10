# UERANSIM Installation Guide - Detailed Explanation

This comprehensive guide outlines the steps and commands necessary for installing UERANSIM on an Ubuntu-based system. Each step is explained in detail to ensure a smooth installation process.

## Prerequisites

Before initiating the installation, make sure your system meets the following requirements:

- Ubuntu 16.04 or a later version
- CMake 3.17 or a later version
- gcc 9.0.0 or a later version
- g++ 9.0.0 or a later version

Note: While other Linux distributions may work, Windows is not supported due to Microsoft's lack of SCTP protocol implementation. Windows users are advised to use a virtual machine.

Here is the [installation of Virtual Machine](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Documentions/Project_Documentation/Ueransim%20%26%20Open5gs%20Installation/00%20Virtual%20Machine%20Installation.md) instructions for Mac & Windows.

## Step 1: Clone the UERANSIM Repository

Use the following command to clone the UERANSIM repository to your home directory:

```bash
cd ~
git clone https://github.com/aligungr/UERANSIM
```

This command downloads the latest UERANSIM source code to your machine.## Step 1: Clone the UERANSIM Repository

To acquire the UERANSIM source code and set up the development environment, follow the steps below:

### Navigate to Home Directory

Open a terminal and change to the home directory using the following command:

```csharp
cd ~
```

### Clone UERANSIM Repository

Clone the UERANSIM repository from the official GitHub repository using the following command:

```csharp
git clone https://github.com/aligungr/UERANSIM
```

This command downloads the latest version of UERANSIM to your local machine.

Now, you have successfully cloned the UERANSIM repository and can proceed with modifying or exploring the source code based on your requirements.

## Step 2: Install Dependencies
Updating System Dependencies
Before proceeding with the installation of UERANSIM, ensure that your system dependencies are up-to-date. Follow these commands to update and upgrade your system:

**Update Package Lists**

```csharp
sudo apt update
```
This command updates the package lists, ensuring that your system has information about the latest available packages.

**Upgrade Installed Packages**

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





