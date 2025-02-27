# An Overview of the Open5GS 5GC Simulation Mobile Network

![image](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/assets/116576484/7cee1426-475f-4ee4-bd2d-c72d3ac48a69)


### Components:
**AMF - Access and Mobility Management**,  **AF - Application Function**, **UDM - Unified Data Management**, **NSSF - Network Slice Selection Function**, **SMF - Session Management Function**, **NEF - Network Exposure Function**, **NRF - Network Repository Function**,**SGW - Serving Gateway**,**PGW - Packet Data Network Gateway**.

# Control Plane and User Plane Network Architecture

## Control Plane
The Control Plane is responsible for managing, signaling, and controlling a telecommunications network.

### Important Functions of the Control Plane
- **Session Management:** Manages the establishment and maintenance of network sessions.
- **Mobility Management:** Manages user device mobility across network cells.
- **Routing Decisions:** Determines pathways for data transmission.
- **Authentication and Authorization:** Verifies user identities and access rights to services.
- **Signaling:** Facilitates the communication necessary for network connection creation and administration.

### Mobile Network Components
- In 4G networks, components such as the **Mobility Management Entity (MME)** are used.
- In 5G networks, components such as the **Access and Mobility Management Function (AMF)** are used.

## User Plane
The User Plane, also known as the Data Plane, is responsible for transmitting user data across the network.

## Important Functions of the User Plane
- **Data Transfer:** Responsible for sending user-generated data.
- **Data Routing and Forwarding:** Manages the sending and receiving of data packets.
- **Data Integrity and Security:** Ensures the security and integrity of data through packet inspection and filtering.

## Mobile Network Components in the User Plane
- In 4G networks, components such as the **Serving Gateway User Plane (SGWU)** and **Packet Gateway User Plane (PGWU)** are used.
- In 5G networks, the **User Plane Function (UPF)** is an important component.

## Interrelationship between Control Plane and User Plane
- **Interdependence:** While they operate separately, the Control Plane and User Plane are interconnected. The Control Plane's management of network connections is crucial for the User Plane's data transmission functions.
- **Separation for Efficiency:** Modern network architectures emphasize the separation of these planes to enhance efficiency, scalability, and flexibility. This division allows for more efficient data handling and improved network management.

# Open5GS 4G/5G NSA Core Components

1. **MME (Mobility Management Entity)**:The MME is a key control-node for the LTE network. It is responsible for initiating paging and authentication of the user, which involves signaling procedures of the LTE network including bearer activation/deactivation and selection of the SGW.
   - **Plane:** Control
   - **Function:** Manages session states, mobility handling, paging, and bearer services. Connects to eNBs (4G base stations).
   - **Picture:** [MME](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Project%20Setup/Results/mmed%20activation.png)
2. **HSS (Home Subscriber Server)**:The HSS is a central database that contains user-related and subscription-related information. It handles the authentication and authorization of subscribers and provides information about the subscribers' location and IP information.
   - **Plane:** Control
   - **Function:** Acts as a central database for user-related and subscription-related information. Manages SIM authentication and holds subscriber profiles.
   - **Picture:** [HSS](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Project%20Setup/Results/hssd%20activation.png)
3. **PCRF (Policy and Charging Rules Function)**:The PCRF is responsible for policy control decision-making, as well as for controlling the flow-based charging functionalities in the policy control framework.
   - **Plane:** Control
   - **Function:** Responsible for policy control decision-making and flow-based charging functionalities in the network.
   - **Picture:** [PCRF](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Project%20Setup/Results/pcrfd%20activation.png)
4. **SGWC (Serving Gateway Control Plane)**:The SGWC is responsible for the control plane functions related to subscriber and session management. It manages and stores data session information during handovers.
   - **Plane:** Control
   - **Function:** Manages data sessions by setting up bearers and routing data within the serving gateway.
5. **SGWU (Serving Gateway User Plane)**:The SGWU is responsible for the user plane functions, which include routing and forwarding user data packets, while also acting as the mobility anchor for the user plane during inter-eNodeB handovers.
   - **Plane:** User
   - **Function:** Handles user data traffic, routing, and forwarding packets to and from mobile devices.
6. **PGWC/SMF (Packet Gateway Control Plane / Open5GS SMF)**:The PGWC/SMF controls the establishment and maintenance of the data network connections and IP address allocation for mobile equipment. In Open5GS, the SMF replaces the PGWC functionality.
   - **Plane:** Control
   - **Function:** Manages data sessions and interfaces with the external internet as part of the packet gateway.
7. **PGWU/UPF (Packet Gateway User Plane / Open5GS UPF)**:The PGWU/UPF is responsible for the IP packet processing and forwarding in the user plane. It performs packet routing and forwarding, QoS enforcement, and serves as the anchor for mobility between LTE and other 3GPP networks.
   - **Plane:** User
   - **Function:** Deals with data packet routing and forwarding in the user plane of the packet gateway.
8. **NRF (NF Repository Function)**: The NRF maintains profiles of network functions and supports their discovery and selection within the network by other network functions.
   - **Plane:** Control
   - **Function:** Maintains profiles of Network Functions (NFs) and supports their discovery within the network.
   - **Picture:** [NRF](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Project%20Setup/Results/nrf%20activation.png)
9. **SCP (Service Communication Proxy)**:The SCP facilitates communication between network functions, particularly when direct communication is inefficient or not possible. It acts as an intermediary to optimize signaling and control traffic.
   - **Plane:** Control
   - **Function:** Facilitates indirect communication between network functions for efficient signaling and data transfer.
   - **Picture:** [SCP](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Project%20Setup/Results/scpd%20activation.png)
10. **SEPP (Security Edge Protection Proxy)**:The SEPP secures the edge of the provider's network, particularly in roaming scenarios. It is responsible for the security of the signaling and interconnect functions.
    - **Plane:** Control
    - **Function:** Enhances security in interconnect scenarios, particularly for roaming interfaces.
11. **AMF (Access and Mobility Management Function)**:The AMF is responsible for access control and mobility management in 5G networks, taking over many of the functions of the MME in 4G.
    - **Plane:** Control
    - **Function:** Manages connection and mobility aspects of the network, similar to the 4G MME's functions.
    - **Picture:** [AMF](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Project%20Setup/Results/amf%20activation.png)
12. **SMF (Session Management Function)**:The SMF manages session states and performs control plane functions related to session management in the 5G network.
    - **Plane:** Control
    - **Function:** Responsible for session management, akin to a combination of MME/SGWC/PGWC functions in 4G.
    - **Picture:** [SMF](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Project%20Setup/Results/smf%20activation.png)
    - **Understanding SMF:**
    - SMF is a Control Plane(CP) function that manages the session-related context with the UPF. It creates, updates, and removes sessions. It also allocates the IP addresses to each PDU session. SMF provides all the session parameters and supports the functions of UPF. SMF functions are collectively performed by MME, SGW-U, and PGW-U in the 4G System. This NF enables CUPS(Control and User Plane Separation) which decentralized the control plane and data forwarding components of the 4G System. It obtained all the rules and policies from the PCF through the N7 interface and routed them to UPF to execute them in the respective sessions.
13. **UPF (User Plane Function)**: The UPF handles packet routing and forwarding in the 5G network's user plane, performing similar functions to the PGWU in the 4G network.
    - **Plane:** User
    - **Function:** Handles user plane data, managing packet routing and forwarding between the gNB and external networks.
    - **Picture:** [UPF](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Project%20Setup/Results/upf%20activation.png)
    - **Understanding UPF:**
    - The User Plane Function (UPF) is a crucial component in the 5G Core network, serving as one of its key Network Functions (NF). It plays a significant role as the second network function that interacts with the NR RAN (New Radio Access Network) during the flow of Protocol Data Units (PDUs). The UPF represents the advancement of CUPS (Control and User Plane Separation), a concept integral to network architecture. Its primary functions include inspecting, routing, and forwarding packets within Quality of Service (QoS) flows, adhering to the subscription policies. Additionally, the UPF is responsible for enforcing upstream and downstream traffic rules, utilizing Service Data Flow (SDF) templates provided by the Session Management Function (SMF) through the N4 interface. The UPF also manages the allocation or termination of QoS Flows within the PDU Sessions in response to the commencement or conclusion of corresponding services.
14. **AUSF (Authentication Server Function)**:The AUSF is involved in the authentication procedure in the network, validating the users' credentials and providing the necessary security features.
    - **Plane:** Control
    - **Function:** Manages authentication procedures for the network.
    - **Picture:** [AUSF](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Project%20Setup/Results/ausf%20activation.png)
15. **UDM (Unified Data Management)**:The UDM handles subscriber data management tasks, which includes generating authentication credentials and managing subscriber profiles.
    - **Plane:** Control
    - **Function:** Manages subscriber data and subscription profiles, similar to the 4G HSS.
    - **Picture:** [UDM](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Project%20Setup/Results/udm%20activation.png)
16. **UDR (Unified Data Repository)**:The UDM handles subscriber data management tasks, which includes generating authentication credentials and managing subscriber profiles.
    - **Plane:** Control
    - **Function:** Stores and manages structured and unstructured network data.
    - **Picture:** [UDR](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Project%20Setup/Results/udrd%20activation.png)
17. **PCF (Policy and Charging Function)**: The PCF is responsible for policy control and provides rules for data charging.
    - **Plane:** Control
    - **Function:** Responsible for policy control and charging rules.
    - **Picture:** [PCF](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Project%20Setup/Results/pcf%20activation.png)
18. **NSSF (Network Slice Selection Function)**:The NSSF is responsible for selecting the network slice instance to serve the user equipment based on the user's service requirements.
    - **Plane:** Control
    - **Function:** Selects the appropriate network slice based on service requirements.
    - **Picture:** [NSSF](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Project%20Setup/Results/nssf%20activation.png)
19. **BSF (Binding Support Function)**: The BSF supports the binding of application layer to communication sessions, aligning the application's needs with the network's capabilities.
    - **Plane:** Control
    - **Function:** Supports binding of the application layer with the communication session.
    - **Picture:** [BSF](https://github.com/FRA-UAS/mobcomwise23-24-team_5gtechtribe/blob/main/Project%20Setup/Results/bsfd%20activation.png)

- The instructions you've provided are for setting up and running the Control Plane (C-Plane) and User Plane (U-Plane) components of Open5GS 5G Core (5GC) network. Open5GS is an open-source project implementing the 5G Core and EPC (Evolved Packet Core) of the 3GPP specifications for 4G and 5G mobile networks.

### Running Open5GS 5GC Control Plane (C-Plane)

1. **Start the NRF (Network Repository Function)**:
   ```csharp
   ./install/bin/open5gs-nrfd &
   ```
2. **Start the SCP (Security Protection Proxy)**:
   ```csharp
   ./install/bin/open5gs-scpd &
   ```
3. **Start the AMF (Access and Mobility Management Function)**:
   ```csharp
   ./install/bin/open5gs-amfd &
   ```
4. **Start other components of the C-Plane**:
   - SMF (Session Management Function)
   - AUSF (Authentication Server Function)
   - UDM (Unified Data Management)
   - UDR (Unified Data Repository)
   - PCF (Policy Control Function)
   - NSSF (Network Slice Selection Function)
   - BSF (Binding Support Function)

   These components are started without a delay:
   ```csharp
   ./install/bin/open5gs-smfd &
   ./install/bin/open5gs-ausfd &
   ./install/bin/open5gs-udmd &
   ./install/bin/open5gs-udrd &
   ./install/bin/open5gs-pcfd &
   ./install/bin/open5gs-nssfd &
   ./install/bin/open5gs-bsfd &
   ```

### Running Open5GS 5GC User Plane (U-Plane)

After setting up the C-Plane, you proceed with the U-Plane:

1. **Start the UPF (User Plane Function)**:
   ```csharp
   ./install/bin/open5gs-upfd &
   ```

This setup assumes that Open5GS is already installed and configured on your system. The commands you've provided are executed in a Linux shell (like Bash), and the ampersand (`&`) at the end of each command indicates that the process should run in the background, allowing the next command to be executed without waiting for the previous one to finish.

It's important to ensure that your system meets the necessary requirements and that Open5GS is configured correctly for your network environment. The configuration files for each component would typically be located in the Open5GS config directory and should be set up according to your network specifications.


### Running all Open5gs NFs
Rather than executing each of the open 5GS commands individually, simply use the following command in the terminal:

```csharp
./install/bin/open5gs-nrfd & ./install/bin/open5gs-scpd & ./install/bin/open5gs-amfd & ./install/bin/open5gs-smfd &./install/bin/open5gs-upfd & ./install/bin/open5gs-ausfd & ./install/bin/open5gs-udmd & ./install/bin/open5gs-pcfd & ./install/bin/open5gs-nssfd & ./install/bin/open5gs-bsfd & ./install/bin/open5gs-udrd & ./install/bin/open5gs-mmed & ./install/bin/open5gs-sgwcd & ./install/bin/open5gs-sgwud & ./install/bin/open5gs-hssd & ./install/bin/open5gs-pcrfd
```
