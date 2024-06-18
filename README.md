# Active Directory Lab Overview
![Active Directory Lab](https://i.imgur.com/2BOPubi.png)
## Introduction

In this lab, I utilized VirtualBox to simulate an Active Directory environment using Windows Server 2019 and Windows 10 virtual machines. The process involved configuring IP Addressing, DNS, AD DS, NAT/RAS, and DHCP. I then employed a PowerShell script to create 1,000 users in Active Directory. Finally, I set up a Windows 10 client machine, connected it to the virtual network, and added it to Active Directory.

## Process


### Setting Up the Environment

1. **Download and Install VirtualBox and ISOs**:
   - Downloaded VirtualBox along with ISOs for Windows Server 2019 and Windows 10.

2. **Configure the Domain Controller (Server 2019)**:
   - Created a virtual machine for the Domain Controller (DC) with two network adaptors: one for external internet connection (NAT) and one for the VirtualBox private network (internal).

3. **Configure IP Addressing**:
   - Set up IP addressing for the internal network.

4. **Set Up Active Directory Domain Services**:
   - Assigned the Server 2019 machine as the DC with the domain `mydomain.com`.
   - Created an Organizational Unit (OU) named `_ADMINS` and added myself as a domain administrator.

### Network Configuration

5. **Install RAS/NAT**:
   - Enabled the Windows 10 client to access the internet through the DC by setting up RAS/NAT.
   - Installed Remote Access and configured NAT to allow internal clients to use a single public IP address for internet access.

6. **Set Up DHCP Server**:
   - Configured a DHCP server on the DC to provide IP addresses within a specified range and subnet mask.
   - Used the DC's IP address as the default gateway in DHCP settings.

### Automating User Creation

7. **Automate User Creation with PowerShell**:
   - Utilized a PowerShell script to create 1,000 users in Active Directory.
   - Generated random names using a script and stored them in a `.txt` file for easy access during user creation.
   - **Important**: Set the execution policy to unrestricted before running the PowerShell script using the command: `Set-ExecutionPolicy Unrestricted`.

### Final Steps

8. **Set Up Windows 10 Client**:
   - Created a second virtual machine running Windows 10, named `client1`.
   - Verified network connectivity and DNS functionality by using `ipconfig` and `ping` commands to ensure proper NAT and internet access.


## Conclusion

This lab highlighted the power and efficiency of PowerShell in automating administrative tasks, such as creating users in Active Directory. The setup provided valuable experience in managing a server environment and configuring network services. I look forward to refining and simplifying these processes further in future iterations of this lab.
