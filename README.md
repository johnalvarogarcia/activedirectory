# Active Directory Lab Overview

## Introduction

In this lab I used two virtual machines on VirtualBox to simulate an Active Directory environment using Windows Server 2019, and Windows 10. After configuring IP Addressing, DNS, AD/DS, NAT/RAS, and DHCP, I use a PowerShell script to create 1000 users in Active Directory. Finally, we create a client machine on Windows 10 to connect to the virtual network and add it to Active Directory. 

## Process

First, I downloaded VirtualBox and an ISO for both Windows Server 2019 and Windows 10. The first virtual machine I downloaded is the Domain Controller (Server 19), which will house Active Directory. The DC houses 2 network adaptors, the first is to connect to the outside internet, and the second is to connect to the VirtualBox private network. You must make sure to assign 2 adaptors to the DC virtual machine in settings, the first using NAT, and the second dedicated to the internal network.

Next, I set up IP Addressing for the internal network. After that, I set up Active Directory Domain Services and assign the Server 2019 machine as the DC using the domain: mydomain.com. Once the domain is created, I create an Organizational Unit named _ADMINS to add myself as a domain administrator.

The third step is to install RAS/NAT to allow the Windows 10 client (second VM) to be on the private virtual network, but still be able to access the internet via the DC. To do this, go to add roles & features > remote access > routing > install. Once completed, go to routing and remote access from server manager to install NAT (this allows internal clients to access internet using one public IP address).

Once RAS/NAT is set up, we will set up a DHCP server on the DC with the scope information pictured at the top. To do this, we go to add roles & features > DHCP Server > install. We can now go to tools > DHCP in order to set up the scope to give IP addresses in the range with the correct subnet mask. In DHCP settings we will use the DC IP address as the default gateway. 

This is my favorite part where we will use a PowerShell script to add 1000 users to Active Directory. To make it easier, we used a random name generator script to add the 1000 names to a .txt file. This way we can easily call on that text file in the PowerShell script.

Important: you must enter the command below before running the powershell script, or it will not work:

Set-ExecutionPolicy Unrestricted

Now that the script has run and there are 1000 users in Active Directory, you can mess around adding people to different Organizational Units and assigning different permissions, etc. 

The final step is to create the second virtual machine running Windows 10. I named it client1 for simplicity. Once the second VM is up and running, I go to the command prompt and type: ipconfig, then: ping www.google.com.
This is to make sure the DNS server is working and the DC is properly NATTING and forwarding traffic to the internet, and then returning the ping back to the client machine.

## Conclusion

In conclusion, PowerShell is a powerful tool to do many tasks and in this case it saved me a ton of legwork in creating users in my Active Directory to mess around with and assign different permissions. There is a lot of flexibility with this lab in managing a server and I plan to continue to redo the lab many times to find new ways of simplifying tasks.
