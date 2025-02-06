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
  
- We will begin this portion, with signing up and adding a resource group to our Azure account. In order to do this, go ahead and head to portal.azure.com, you will be redirected to a website where you will need a microsoft account. Once created, go ahead and follow the account creation prompts to finalize the account.

![image](https://github.com/user-attachments/assets/04013e04-1827-4102-96d8-ca2cb3b6b0b8)

- Once the account has been created, you will be redirected to the home page.
On the home page make sure to search and or select the button labeled as resource group. Once selected, we will click on 'create' and begin the creation of our new resource group.

![image](https://github.com/user-attachments/assets/f2a3586c-0ed4-4380-bd0f-3907c8186123)
![image](https://github.com/user-attachments/assets/f68e2b78-e317-400b-840d-4f015140a7cc)

- Once you click on 'create' the browser will then give you the following options.

![image](https://github.com/user-attachments/assets/68523612-604d-4c17-a639-331dd9460ebc)

- Make sure, the correct Azure subscription is selected. Then make sure to give the resource goup a name. Once it has been given a name, choose the region you want the resource group to store its data. Once done, go ahead and click on 'next', where it will take you to the 'Tags' section. We can go ahead and leave the tags portion blank, if you would like to go ahead and make changes make sure to do so.

![image](https://github.com/user-attachments/assets/fbd443eb-45bc-40ab-81f9-7ada11176637)

- If you are ready go ahead and click on 'review + create'. It will validate the resource group, then once validated it will let you 'create' the resource group.

![image](https://github.com/user-attachments/assets/533b12d0-4952-4369-b2c1-c138477790a5)

- Now you have created your first resource group! Go ahead and follow to the next steps to continue on with the lab.

</p>

<br />

<h3>Creating Virtual Machines via Azure Portal</h3>

<p>

![image](https://github.com/user-attachments/assets/d6e20364-4da6-4386-ae90-317d63383304)

</p>
<p>
  
- We are creating Virtual Machines via the Azure Portal. We need to make sure that they are both created within the same resource group. We are making sure to create a Virtual Machine on Windows 10 Pro Image, and Linux Ubuntu Image. The following settings should be similar for both virtual machines created. Once both virtual machines have been created, and then deployed; we will be moving onto step number 2.

![image](https://github.com/user-attachments/assets/565bf77c-9e56-4ca0-8c4a-bee5fe61f980)

</p>
<br />
<h3>Installing Wireshark on Windows Virtual Machine</h3>

<p>
  
- In order to get started, we will be using Remote Desktop for windows. You will be remoting into your Windows VM. Make sure to use all settings provided via the virtual machines button on Azure Portal. Once you are in the virtual machine we will be installing wireshark. Make sure to make your way to wireshark.org and download the x64 Windows Installer. Make sure to also install Pcap, NOT USB pcap. Once installed we can move onto the next steps of the lab.

![image](https://github.com/user-attachments/assets/c20ea961-4bc6-446a-8f2f-d2b6024ed594)

<h3>Observing Network Traffic (ICMP)</h3>

</p>
<p>
  
- Once wireshark is installed, make sure to select the 'ethernet' option that shows internet traffic via the graph. Once selected, click on the sharkfin at the top left and a filter for icmp packets. Wireshark should look like this.

![image](https://github.com/user-attachments/assets/556a02aa-f22e-4d77-b0d2-b12b9cd989a5)

- Go ahead and find the private Ip Address of the linux VM. Once found, go to the windows VM and ping the IP address via Powershell. 'ping 10.0.0.x' The command should send out 4 packets to the linux VM, whereas on wireshark you will see 8 prompts.

![image](https://github.com/user-attachments/assets/735fbf24-4176-4a8c-8b1b-2ee676c7f52d)

- These 8 prompts signify that with every request sent out to that private IP address, there was a reply. Therefore the connection is working.

- You can also see the Mac Address of the computer you are using by clicking on one of the packets on wireshark, then going to 'Ethernet II' and under 'Source' the physical address will be shown. This is also the Data Link Layer of the OSI model at work. This can also be confirmed via powershell.

![image](https://github.com/user-attachments/assets/38299048-743f-4585-bb97-06f26a2f1c3e)

- If we were to expand the 'Internet Protocol Version 4' section of wireshark, this is representative of the Network Layer in the OSI Model.

![image](https://github.com/user-attachments/assets/56508728-1ce9-46aa-8646-ed6216b82743)

</p>
<br />

<h3>Configuring a Firewall using Network Security Groups</h3>

<p>

- Now, we will be going back into the Azure Portal to change the Network Security group. Before we do this, we need to make sure the Windows 10 VM that we have open is constantly pinging the linux vm. Using the command 'ping 10.0.0.x -t', this will make sure the ping command keeps pinging the linux vm we have set in place. Afterwards, go ahead and navigate to ur linux vm, then go to Network Settings under Networking; and here the Network security group will be shown.

![image](https://github.com/user-attachments/assets/74488dc0-16b3-4cbb-9b2f-fee2bcca181d)

- Now make sure to click on: 'linux-vm-nsg' or what your security group is named. From here we will be adding an incoming rule, as our goal is to block the pings from being sent to the Linux VM. In order to get to adding the rule, you will navigate to the security groups settings -> then Inbound security rules -> and lastly add. From here we will configure the rule to block and ICMP traffic. 

![image](https://github.com/user-attachments/assets/9f84779a-f832-415b-b009-77028944ce0c)

- Once the rule has been added, and the rule begins to work; the packets being sent to the VM will be blocked. There will be no reply handled on wireshark and the request will be timed out on powershell.

![image](https://github.com/user-attachments/assets/18f230fe-1052-4c38-894d-a4290c4b96dc)
![image](https://github.com/user-attachments/assets/2e0365de-f7ad-4198-aa3a-758b0f00d0d8)

- Now, we will delete the rule and you will see that the traffic will go back to normal. Once the powershell packets stop being timed out, go ahead and press ctrl+c to stop the process altogether.

<h3>Observing Network Traffic (SSH)</h3>

</p>
<p>
  
- Make sure to have the windows 10 virtual machine open. Once open, make sure to filter the packets on wireshark to only show 'ssh' traffic. 

![image](https://github.com/user-attachments/assets/243c2492-0f02-456e-a133-331cdeb98ac0)

- Once, you have filtered the wireshark packet capture; we will now begin to ssh into the linux vm using the windows 10 vm. In order to do this, you need to open powershell and type the following prompt: 'ssh username@private IP Address'. Make sure to fill in any required information. It will prompt you to enter the password for the username, once entered you will have successfuly entered the linux machine via the CLI.

![image](https://github.com/user-attachments/assets/e9f2cf89-ca89-4ca7-bb49-3c9982f2f526)

- The instance you begin to type into the Linux command line interfacem the wireshark will begin tracing the ssh packets being sent. We cannot access the payload when it comes to ssh packets as they are encrypted. (Port 22 is used for ssh; you can also filter traffic by using 'tcp.port = = 22').

![image](https://github.com/user-attachments/assets/0232b11d-3911-4d64-bde9-7b6d55f451df)
![image](https://github.com/user-attachments/assets/988a64aa-146f-40e5-b38a-31f208d1e442)

- After examining some of the packets, we can now exit the command line interface by typing 'exit' into powershell and pressing enter.

</p>

<h3>Observing Network Traffic (DHCP)</h3>
<p>
  
- We will begin this section by applying the filters to wireshark via the Windows 10 virtual machine. The filter applied will be 'dhcp'. We will then create a script, to properly see all the packets that go into assigning an IP via the DHCP.

- Open up notepad, and type in the following text:
  ipconfig /release
  ipconfig /renew
  ![image](https://github.com/user-attachments/assets/34aa1039-cc34-4939-87cd-165b6f330c2b)

- Make sure to save as, and in the file search type: 'c:/programdata' and hit enter. This is where we will store the file. Change the filetype to 'all types' and name the file 'dhcp.bat'. It should now look like this.
![image](https://github.com/user-attachments/assets/6657d714-b2a7-4a96-8a8c-922d444d19d5)

- You will now save the file, and close out of the notepad. Open powershell in administator, once here we will be using 2 commands. 'CD' or 'change directory' and 'LS' or 'list files'. The first prompt will be to move the directory of powershell into where you have stored the .bat file script. The prompt should be the following: 'cd c:\programdata' then press enter. Now if you type the command 'ls', you should see a list of files within that directory. From here we will run the bat file.

![image](https://github.com/user-attachments/assets/2a6c0f73-c614-4466-b19b-cac4669e783e)

- Make sure, that wireshark is currently caputing packets. Now that we know wireshark is running we will type: '.\dhcp.bat' this will run the file and create the packets we need. Be aware the connection will be lost; but our script will immediately renew the connection. Once renewed, you should have a total of 5 packets within wireshark.

![image](https://github.com/user-attachments/assets/5d8e548f-6a8d-45dc-9d40-1b3cb69ebe64)

- Now a side explanation, 'ipconfig /release' sent out the first packet shown as release in wireshark. However since 'ipconfig /renew' was ran right after it, we still were able to connect soon after. Our VM being the source of 0.0.0.0, is sending out a "broadcast" to the dhcp server; this can be seen as 255.255.255.255 where the source discovers the DHCP server. Once it was discovered, the DHCP server sent out an offer request to our VM, which then the VM sent back a request packet. The last packet is showing that both the source and destination acknowledge each other.

</p>

<h3>Observing Network Traffic (DNS)</h3>

<p>
  
- We are now going to be changing the filter onto wireshark to 'DNS'. Make sure to clear any old packets, and we will start creating our own traffic. Now in powershell, we will be using the command: 'nslookup google.com'; this will tell us the IP address of google.com and in turn give us DNS traffic.

![image](https://github.com/user-attachments/assets/533aacfa-0459-4757-b171-a945eb36f6fe)
</p>

<h3>Observing Network Traffic (RDP)</h3>

<p>
  
- We will now be filtering wireshark to track any RDP traffic. We will need to put this into the filter for wireshark. 'tcp.port == 3389'

![image](https://github.com/user-attachments/assets/c61d6dc8-9940-4513-9e60-9dbc19ec34ac)

- Now above once filtered, you will see that the traffic is constant. This is because, we are currently using remote desktop protocol. Since we are constantly receiving an image from the virtual machine, the packets will constantly be sent over the network.


</p>

<br />
