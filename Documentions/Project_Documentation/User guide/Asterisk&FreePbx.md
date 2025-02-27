
# 1. Asterisk

# Detailed Guide on Installing Asterisk on Ubuntu 22.04

Asterisk is a leading open-source software that acts as the backbone for a wide array of communication solutions, including IP PBX systems, conference servers, and VoIP gateways. Its global adoption across various scales of businesses can be attributed to its rich set of features and the flexibility it offers. This detailed guide aims to walk you through the process of installing Asterisk on Ubuntu 22.04, ensuring you have a robust setup ready for your communication needs.

## Why Choose Asterisk?

### Cost Savings
Asterisk's open-source nature eliminates licensing costs associated with commercial communication systems, providing a cost-effective solution for businesses. Its adaptability means you can tailor the system to your needs without additional financial investment in proprietary software.

### Unparalleled Flexibility
Asterisk's compatibility with diverse technologies and programming languages allows for the development of customized communication applications. Whether you're integrating with existing systems or building from scratch, Asterisk provides the flexibility needed for innovative telephony solutions.

### Customizability and Scalability
With Asterisk, the power to customize and scale your communication setup is in your hands. It supports a wide range of telephony hardware and can be configured to handle anything from a few calls to thousands of concurrent connections, making it an ideal choice for businesses of any size.



## Prerequisites for Installing Asterisk

Before proceeding with the installation, ensure you have:
- A machine or virtual environment running Ubuntu 22.04.
- At least 1 GB of RAM and one or more CPU cores to support the operation.
- Sudo privileges to execute necessary commands.

## Installation Steps

### Step 1: System Preparation

1. **Update and Upgrade:**
   Begin by refreshing your system's package list and upgrading outdated packages to reduce potential conflicts during installation.

   ```bash
   sudo apt-get update
   sudo apt-get upgrade
   ```

2. **Install Dependencies:**
   Asterisk requires several build tools and libraries to compile from source. Install these dependencies to ensure a smooth setup.

   ```bash
   sudo apt-get install build-essential git-core subversion wget libjansson-dev sqlite autoconf automake libxml2-dev libncurses5-dev libtool
   ```

### Downloading and Extracting Asterisk

- **Navigate to the Source Directory:**
  The `/usr/src` directory is commonly used for source files. Change to this directory before downloading Asterisk.

  ```bash
  cd /usr/src/
  ```

- **Download Asterisk:**
  Fetch the latest version of Asterisk. This guide uses version 20 as an example, but you should check for the most current version available.

  ```bash
  sudo wget http://downloads.asterisk.org/pub/telephony/asterisk/asterisk-20-current.tar.gz
  ```

- **Extract the Tarball:**
  Once downloaded, extract the contents to proceed with the installation.

  ```bash
  sudo tar zxf asterisk-20-current.tar.gz
  cd asterisk-*/
  ```

### Step 2: Resolving Dependencies

1. **MP3 Module Preparation:**
   If you intend to use MP3 files with Asterisk, execute the script to download necessary MP3 sources.

   ```bash
   sudo contrib/scripts/get_mp3_source.sh
   ```

2. **Install Required Packages:**
   Run the provided script to automatically install all dependencies required by Asterisk on Ubuntu 22.04.

   ```bash
   sudo contrib/scripts/install_prereq install
   ```


### Step 3: Compiling Asterisk

1. **Configure the Build:**
   Run the configure script to check for all required dependencies and set up the build environment.

   ```bash
   sudo ./configure
   ```

2. **Module Selection:**
   Use the `make menuselect` command to choose which modules you'd like to compile and include in your Asterisk installation.

   ```bash
   sudo make menuselect
   ```

3. **Compile:**
   Compile Asterisk with the `make` command. Adjust the `-j` flag based on your processor's core count to speed up the compilation process.

   ```bash
   sudo make -j2
   ```

4. **Install:**
   After compilation, install Asterisk along with the selected modules.

   ```bash
   sudo make install
   ```

5. **Configuration Samples:**
   Install sample or basic PBX configuration files to help you get started with Asterisk.

   ```bash
   sudo make samples
   sudo make basic-pbx
   ```

6. **Init Script:**
   Set up the Asterisk init script for easy service management.

   ```bash
   sudo make config
   sudo ldconfig
   ```

### Step 4: Running Asterisk Securely

1. **Create a Dedicated User:**
   For security reasons, it

's best to run Asterisk under a dedicated non-root user.

   ```bash
   sudo adduser --system --group --home /var/lib/asterisk --no-create-home --gecos "Asterisk PBX" asterisk
   ```

2. **Adjust Permissions:**
   Ensure the Asterisk user has the appropriate permissions for all necessary files and directories.

   ```bash
   sudo chown -R asterisk: /var/{lib,log,run,spool}/asterisk /usr/lib/asterisk /etc/asterisk
   sudo chmod -R 750 /var/{lib,log,run,spool}/asterisk /usr/lib/asterisk /etc/asterisk
   ```

### Step 5: Launching and Managing Asterisk

1. **Start the Service:**
   Kickstart the Asterisk service and verify it's running smoothly.

   ```bash
   sudo systemctl start asterisk
   sudo asterisk -vvvr
   ```

2. **Enable at Boot:**
   Ensure Asterisk automatically starts with your system.

   ```bash
   sudo systemctl enable asterisk
   ```

### Step 6: Firewall Configuration

To protect your server and manage traffic efficiently:

1. **SIP Traffic:**
   Open the default SIP port if you're using SIP protocol.

   ```bash
   sudo ufw allow 5060/udp
   ```

2. **RTP Traffic:**
   Open the necessary port range for RTP traffic, essential for voice data transmission.

   ```bash
   sudo ufw allow 10000:20000/udp
   ```


# 2. Kamailio Server Installation Guide
Before proceeding with the installation, ensure you have:
- A machine or virtual environment running Ubuntu 22.04
- At least 1 GB of RAM and one or more CPU cores to support the operation.
- Sudo privileges to execute necessary commands.

### Step 1 – Install Required Dependencies

```bash
sudo apt-get install gnupg2 mariadb-server curl unzip -y
   ```
### Step 2 – Install Kamailio Server

```bash
wget -O- http://deb.kamailio.org/kamailiodebkey.gpg | sudo apt-key add -
sudo nano /etc/apt/sources.list.d/kamailio.list
   ```
```bash
deb http://cz.archive.ubuntu.com/ubuntu bionic main
deb http://deb.kamailio.org/kamailio53 bionic main
deb-src http://deb.kamailio.org/kamailio53 bionic main
   ```

```bash
sudo apt-get update -y
sudo apt-get install kamailio kamailio-mysql-modules kamailio-websocket-modules kamailio-tls-modules -y
kamailio -V
   ```

### Step 3 – Configure Kamailio

```bash
sudo nano /etc/kamailio/kamctlrc
sudo kamdbctl create
sudo nano /etc/kamailio/kamailio.cfg
   ```
```bash
#!define WITH_MYSQL
#!define WITH_AUTH
#!define WITH_USRLOCDB
#!define WITH_ACCDB
   ```

### Step 4 – Install Siremis Dashboard

****work in progress****





# 3. FreePBX

# Comprehensive FreePBX Installation and Configuration Manual for Ubuntu 22.04 / 23.04

## Introduction to FreePBX

FreePBX stands as a pinnacle of open-source IP PBX administration tools, developed with the expertise of Sangoma Technologies. It's designed with the foresight to empower corporate communication systems, offering a plethora of customization options. This includes a vast array of pre-installed functionalities and the liberty to incorporate additional modules, thus providing a scalable solution that can be tailored to meet the intricate requirements of any business. This manual aims to guide you through the detailed process of installing and configuring FreePBX on Ubuntu versions 22.04 and 23.04, ensuring a smooth and efficient setup.

## Distinguishing Features of FreePBX

FreePBX is equipped with an impressive suite of features designed to enhance and streamline your telephony infrastructure:

- *Security Updates Notification:* A proactive feature ensuring the system remains safeguarded against new vulnerabilities and threats, thereby maintaining integrity and reliability.
- *Expandability:* The system's functionality can be significantly enhanced with additional features such as high availability setups, comprehensive call center packages, and integration with IP phones, making it a versatile choice for diverse telephony needs.
- *Intuitive Web GUI:* The platform boasts a full-featured web interface, simplifying complex tasks such as configuration, management, and updates, making it accessible even to those with minimal technical expertise.
- *Localization Support:* Offers customization of the endpoint devices' local language, ensuring a user-friendly experience for diverse geographical deployments.
- *Comprehensive Communication Setup:* Facilitates the easy setup of extensions, users, queues, and interactive voice responses (IVRs), allowing for a tailored communication structure.
- *Open-Source Framework:* The openly available source code not only fosters innovation but also ensures a transparent and collaborative approach to telecommunication solutions.
- *Plugin Management Ease:* The system allows for straightforward addition and modification of plugins, enhancing functionality and user experience.
- *Backup and Restoration Simplicity:* Features robust tools for data backup and recovery, ensuring business continuity and ease of data management.
- *Detailed Call Management:* Access to detailed call logs and recordings through the ARI in Asterisk, offering valuable insights and compliance capabilities.
- *Music on Hold and Call Redirection:* Personalizes the caller experience with customizable music on hold and intelligent call redirection based on time-of-day or other criteria.
- *Universal Compatibility:* Ensures compatibility with all trunk technologies supported by Asterisk, providing flexibility in telephony infrastructure design.

## Installation Workflow

### Pre-Installation Requirements

- *System Setup:* An operational server running Ubuntu 22.04 or 23.04.
- *Administrative Access:* Root access or a user account with sudo privileges to execute installation commands.

### Step 1: Dependency Installation

Before diving into the FreePBX installation, it's crucial to prepare your system by installing necessary dependencies. This ensures that all required libraries and tools are available for both Asterisk and FreePBX:

1. *System Update:*
   Initiate by updating your system's package list and upgrading existing packages to their latest versions. This step is vital for security and functionality.
    ``` bash
   apt update -y
   apt upgrade -y
     ```

2. *Install Asterisk Dependencies:*
   Asterisk requires several dependencies for its operation. Install these to ensure a smooth compilation process.

     ``` bash
   apt-get install unzip git gnupg2 curl libedit-dev libnewt-dev libssl-dev libncurses5-dev subversion libsqlite3-dev build-essential libjansson-dev libxml2-dev uuid-dev subversion -y
     ```

### Step 2: Asterisk Server Installation

Asterisk serves as the backbone for FreePBX, handling the core PBX functionality. Installing it from source allows for the latest features and fixes:

1. *Download and Extract Asterisk:*
   Fetch the latest version of Asterisk and prepare it for installation.

     ```bash
   wget http://downloads.asterisk.org/pub/telephony/asterisk/asterisk-20-current.tar.gz
   tar -xvzf asterisk-20-current.tar.gz
     ```

2. *Compile and Install Asterisk:*
   Navigate to the Asterisk source directory, install prerequisite packages, configure, and compile Asterisk. This process can take some time, depending on your system's capabilities.

     ```bash
   cd asterisk-20.2.1
   contrib/scripts/get_mp3_source.sh
   contrib/scripts/install_prereq install
   ./configure
   make menuselect
   make -j2
   make install
   make samples
   make config
   ldconfig
     ```

3. *Set User Permissions:*
   For security and operational integrity, it's recommended to run Asterisk under a dedicated user account rather than root.

    ``` bash
   groupadd asterisk
   useradd -r -d

 /var/lib/asterisk -g asterisk asterisk
   usermod -aG audio,dialout asterisk
   chown -R asterisk.asterisk /etc/asterisk
   chown -R asterisk.asterisk /var/{lib,log,spool}/asterisk
   chown -R asterisk.asterisk /usr/lib/asterisk
     ```

### Step 3: LAMP Server Configuration

FreePBX requires a web server, database, and PHP to function. Installing these components forms the basis of the LAMP (Linux, Apache, MySQL/MariaDB, PHP) stack:

1. *Install LAMP Components:*
   Add the PHP repository to get the latest PHP versions, then install Apache, MariaDB, PHP, and necessary PHP extensions.

    ``` bash
   apt install software-properties-common -y
   add-apt-repository ppa:ondrej/php -y
   apt install apache2 mariadb-server libapache2-mod-php7.4 php7.4 and other required PHP modules
     ```

2. *Service Activation:*
   Ensure that Apache and MariaDB services are running and set to start automatically on system boot.

    ``` bash
   systemctl start apache2 mariadb
   systemctl enable apache2 mariadb
     ```

### Step 4: FreePBX Server Deployment

With Asterisk and the LAMP stack in place, you're now ready to install FreePBX, which will interface with Asterisk to provide an extensive PBX management platform:

1. *Download and Install FreePBX:*
   Fetch the latest FreePBX version and initiate the installation script. This process integrates FreePBX with Asterisk and the web server.

    ```bash
   wget http://mirror.freepbx.org/modules/packages/freepbx/freepbx-16.0-latest.tgz
   tar -xvzf freepbx-16.0-latest.tgz
   cd freepbx
   apt-get install nodejs npm -y
   ./install -n
     ```

2. *Configure Apache and PHP for FreePBX:*
   Adjust Apache's user and group to run as Asterisk and modify PHP settings to meet FreePBX requirements. These steps ensure that FreePBX can operate correctly within the web server environment.

     ```bash
   sed -i 's/^\(User\|Group\).*/\1 asterisk/' /etc/apache2/apache2.conf
   sed -i 's/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf
   sed -i 's/\(^upload_max_filesize = \).*/\120M/' /etc/php/7.4/apache2/php.ini
   a2enmod rewrite
   systemctl restart apache2
     ```

### Step 5: Web Interface Access and Configuration

The final step in the FreePBX installation process is accessing the web interface to complete the setup and configuration of your PBX system:

- *Access the FreePBX Administration Interface:*
  Open a web browser and navigate to your server's IP address followed by /admin. This will take you to the FreePBX administration login page, where you can finalize the setup process and start configuring your PBX settings.

## Post-Installation Configuration and Security

After the initial setup, there are several important steps and considerations to ensure your FreePBX system is secure, efficient, and tailored to your needs:

### Secure the Database

It's essential to secure your MariaDB installation to protect your data and prevent unauthorized access:

- Run the mysql_secure_installation script to set a root password, remove anonymous users, disable remote root logins, and drop the test database.

### Firewall Configuration

For security and to ensure proper operation of FreePBX, configure your server's firewall to allow traffic on necessary ports:

- Use UFW or another firewall tool to open ports for HTTP (80), HTTPS (443), SIP (5060), and the RTP range (10000-20000) for voice traffic.

### Email Setup for Notifications

Configure an email server on your FreePBX system to send out notifications and alerts:

- Install and configure Postfix or another MTA (Mail Transfer Agent) to handle outgoing emails from FreePBX.

### Regular Backups

Establish a routine for backing up your FreePBX configuration and data to safeguard against data loss:

- Use the built-in FreePBX Backup & Restore module to schedule regular backups, and consider offsite backups for additional security.

### System Updates and Maintenance

Keep your FreePBX system up to date with regular updates to both FreePBX modules and the underlying Ubuntu system:

- Regularly check for and apply updates through the FreePBX Admin interface and the Ubuntu package manager.

### Explore Additional Modules

FreePBX's functionality can be significantly extended through modules, offering features like call recording, CRM integration, fax

 handling, and more:

- Investigate and install additional FreePBX modules to enhance your PBX's capabilities and customize it to fit your business requirements.
