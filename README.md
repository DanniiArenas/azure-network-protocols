<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (22h2)
- Linux (ubuntu 24.04)

<h2>High-Level Steps</h2>

- Create Azure Virtual Machines
- Observe ICMP Traffic
- Configure Firewalls via Network Security Groups
- Observe Traffic - (SSH, DHCP, DNS, and RDP)

<h2>Actions and Observations</h2>

![image](https://github.com/user-attachments/assets/aa03c752-2126-4069-ac7b-7d5e2733f5fa)
<h3>Getting Started with Azure</h3>

<p>
We will begin this portion, with signing up and adding a resource group to our Azure account. In order to do this, go ahead and head to portal.azure.com, you will be redirected to a website where you will need a microsoft account. Once created, go ahead and follow the account creation prompts to finalize the account.

![image](https://github.com/user-attachments/assets/04013e04-1827-4102-96d8-ca2cb3b6b0b8)

Once the account has been created, you will be redirected to the home page.
On the home page make sure to search and or select the button labeled as resource group. Once selected, we will click on 'create' and begin the creation of our new resource group.

![image](https://github.com/user-attachments/assets/f2a3586c-0ed4-4380-bd0f-3907c8186123)
![image](https://github.com/user-attachments/assets/f68e2b78-e317-400b-840d-4f015140a7cc)

Once you click on 'create' the browser will then give you the following options.

![image](https://github.com/user-attachments/assets/68523612-604d-4c17-a639-331dd9460ebc)

Make sure, the correct Azure subscription is selected. Then make sure to give the resource goup a name. Once it has been given a name, choose the region you want the resource group to store its data. Once done, go ahead and click on 'next', where it will take you to the 'Tags' section. We can go ahead and leave the tags portion blank, if you would like to go ahead and make changes make sure to do so.

![image](https://github.com/user-attachments/assets/fbd443eb-45bc-40ab-81f9-7ada11176637)

If you are ready go ahead and click on 'review + create'. It will validate the resource group, then once validated it will let you 'create' the resource group.

![image](https://github.com/user-attachments/assets/533b12d0-4952-4369-b2c1-c138477790a5)

Now you have created your first resource group! Go ahead and follow to the next steps to continue on with the lab.


</p>

<h3>Creating Virtual Machines via Azure Portal</h3>

<p>

![image](https://github.com/user-attachments/assets/d6e20364-4da6-4386-ae90-317d63383304)

</p>
<p>
We are creating Virtual Machines via the Azure Portal. We need to make sure that they are both created within the same resource group. We are making sure to create a Virtual Machine on Windows 10 Pro Image, and Linux Ubuntu Image. The following settings should be similar for both virtual machines created. Once both virtual machines have been created, and then deployed; we will be moving onto step number 2.

![image](https://github.com/user-attachments/assets/565bf77c-9e56-4ca0-8c4a-bee5fe61f980)

</p>
<br />
<h3>Installing Wireshark on Windows Virtual Machine</h3>

<p>
In order to get started, we will be using Remote Desktop for windows. You will be remoting into your Windows VM. Make sure to use all settings provided via the virtual machines button on Azure Portal. Once you are in the virtual machine we will be installing wireshark. Make sure to make your way to wireshark.org and download the x64 Windows Installer. Make sure to also install Pcap, NOT USB pcap. Once installed we can move onto the next steps of the lab.

![image](https://github.com/user-attachments/assets/c20ea961-4bc6-446a-8f2f-d2b6024ed594)

<h3>Observing Network Traffic</h3>

</p>
<p>
Once wireshark is installed, make sure to select the 'ethernet' option that shows internet traffic via the graph. Once selected, click on the sharkfin at the top left and a filter for icmp packets. Wireshark should look like this.

![image](https://github.com/user-attachments/assets/556a02aa-f22e-4d77-b0d2-b12b9cd989a5)

11

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
