![[Pasted image 20240516080448.png]]

the interface of the cisco packet tracer
- there we have a logical view and physical view in logical view we can see how devices are connected and physical view we can actually view the physical components 
- below we have a list of devices (routers, switches, home devices, cam etc)
- above that we have two options one is if we want to repeat the transmission or something another is fast forward the transmission without waiting for the specific device to initiate or complete the transmission of packets or something

## task -1 
build a home network using cables and devices

![[Pasted image 20240516080934.png]]

we have networking devices starting 
- and below networking devices we have wireless devices then we have a home router we can use that 
![[Pasted image 20240516081139.png]]

Then we have end devices in second here we can select a laptop of pc or other devices we want let's select a PC and a laptop
let's say the home network have a camera 
![[Pasted image 20240516081400.png]]

- again if we click on end devices and click on home we can see camera 
Now let's connect those devices

to connect
![[Pasted image 20240516081606.png]]
if we go to thunder symbol we can see thunder symbol at the starting which is automatic connection type or we can pick normally 
let's go with automatic connection for now 

![[Pasted image 20240516081730.png]]

if we click on laptop we can see all the components and connections physically as we can see laptop default comes with a cable connection if we want the laptop to be a wireless connection for the router then we have to power of the laptop then remove the ethernet card and install the wireless card
- as we can see we have WPC300N is a wifi card 
![[Pasted image 20240516082025.png]]
we've installed the wifi card successfully now let's turn on the laptop again and see if it's connecting to our home router or not 

now connecting to the camera we can't directly connect to the port and router
![[Pasted image 20240516082534.png]]

refer to this :https://stackoverflow.com/questions/71095743/packet-tracer-webcam

![[Pasted image 20240516083032.png]]
we've changed it to ethernet let's conenct the router and the camera now
![[Pasted image 20240516083127.png]]

we have added a ethernet port to our router
![[Pasted image 20240516083153.png]]

A home network is setup and active

Packet Tracer also provides a variety of tabs for device configuration including the following:

- Physical
- Config
- CLI
- Desktop
- Services
![[Pasted image 20240516083558.png]]

The Physical tab provides an interface for interacting with the device including powering it on or off or installing different modules, such as a wireless network interface card (NIC).

![[Pasted image 20240516083609.png]]
For intermediate devices such as routers and switches, there are two ways to access device configurations. Configurations can be accessed via a Config tab, which is a Graphical User Interface (GUI). Configurations can also be accessed using a command line interface (CLI).
- The Config tab does not simulate the functionality of a device
- As settings are changed in the GUI, the equivalent CLI commands appear in the **Equivalent IOS Commands** window.
![[Pasted image 20240516083708.png]]

- provides access to the command line interface of a Cisco device. Using the CLI tab requires knowledge of device configuration with IOS.
- CLI configuration is a necessary skill for more advanced networking implementations.
-  Any commands that were entered from the Config tab are also shown in the CLI tab.
![[Pasted image 20240516083747.png]]

- For some end devices, such as PCs and laptops, Packet Tracer provides a desktop interface that gives you access to IP configuration, wireless configuration, a command prompt, a web browser, and other applications.
![[Pasted image 20240516083759.png]]

- A server has all of the functions of a host with the addition of one more tab, the Services tab. This tab allows a server to be configured with common server processes such as HTTP, DHCP, DNS, or other services, as shown in the figure.

## logical mode and physical mode
![[Pasted image 20240516084236.png]]
in physical mode we can right click on specific device and we can click on inspect front for the front view
example:
![[Pasted image 20240516084352.png]]

![[Pasted image 20240516084452.png]]

we can hover over the port we want to connect after clicking on inpsect front and hover over the port we want to connect and connect to the end devices we want 

## Cisco Packet Tracer File Types

Packet Tracer has the ability to create four different types of files. These file types are used for different purposes and include: .pka, .pkt, .pksz, and .pkz.

### PKA file

- The .pka file type is a Packet Tracer Activity file and is the file type you will experience most often. Think of the “a” in .pka as meaning “activity.”
-  This file type contains two networks: an initial network and an answer network
- The Packet Tracer Activity instructions window provides the procedures required to complete the activity, assignment, or assessment.
### PKT file
- The .pkt file type is created when a simulated network is built in Packet Tracer and saved. The .pkt file can also have graphic background images embedded within it. However, .pkt files have no instructions window or activity scoring.
### PKSZ file
- The .pksz file type is specific to Packet Tracer Tutored Activities (PTTA). These files bundle a .pka file, media assets, and a scripting file for the hinting system. These activities provide support, in the form of contextualized hints, for students who are working on completing the activity.

### PKZ file 
-  This file type was previously used to embed images and other files in a Packet Tracer file. However, images are now embedded directly within a regular .pkt or .pka file by default. Therefore, consider .pkz as a deprecated file type.

![[Pasted image 20240516085345.png]]

## Setting ip address in end devices
![[Pasted image 20240516085707.png]]

if we go to pc and config tab and click on fast eth0 then we can see ip config we can use dhcp or we can assign the ip address statically
![[Pasted image 20240516085811.png]]
above is a DHCP example
or another way is you can click on pc and go to desktop anc click on cmd prompt to see the ip address
![[Pasted image 20240516085909.png]]

since we haven't set any ip address everything will be default 0.0.0.0
![[Pasted image 20240516085951.png]]

![[Pasted image 20240516090210.png]]

### **Create and configure a simple network** 

**Part 1: Build a Simple Network**
**Part 2: Configure the End Devices and Verify Connectivity**

![[Pasted image 20240516091848.png]]

![[Pasted image 20240516091937.png]]

![[Pasted image 20240516092048.png]]

- you can add campus layout and or city maps to configure the networking devices
you can customize icons too
![[Pasted image 20240516092207.png]]


### connect to the console of a device for the purpose of updating the configuration

Part 1: Connect to the Device Using a Console Connection

Part 2: Copy Configuration Information to the Device

Part 3: Save the Updated Configuration to the Device

to access the terminal go to desktop and click on terminal leave the settings default and and click on okay it will open something like this 
- if you want to view all the available commands then u can type ? and click enter 

![[Pasted image 20240517071755.png]]

- to access the root mode we have to type enable and click enter
![[Pasted image 20240517072402.png]]

- as we can see we can see more commands in root mode then in user mode 
- to view the running config on the switch we have to type show running config command
![[Pasted image 20240517072724.png]]

since we haven't setup anything that is the default config 

- to enter configuration mode we have to use the command configure terminal
 ![[Pasted image 20240517073136.png]]
- as we can see we enterd config mode and 
	- we set host name using hostname command
	- line con 0 is typically defining the network cable typically rj-45 something 
	- password is set suing password command
	- login specifies it requires to login everytime 
	- end is using to end the configuration 
now if we exit again and login it will ask for login 
![[Pasted image 20240517073528.png]]

![[Pasted image 20240517073955.png]]

- copy running-config startup-config is used to set running config as startup config 
- reload is used to reload config and startup from starting
- it will again ask password to login and the configuration we changed is saved as startup config
![[Pasted image 20240517074936.png]]

- there is simulation mode in the packet tracer which allows user to see the flow of packets through entire network and the play button is used to send packet and forward and backward buttons are used to speed up or go back and repeat the process
![[Pasted image 20240517075224.png]]
- we have a option called edit filters packets and we have 3 options namely IPv4 IPv6 Misc types and we can select different options to send different packets from each mode
- we can experiment with delaying packets and send only specific number of packets with PDU
![[Pasted image 20240517080001.png]]

- here after simulations if we view the previous event details we can see that there are different packets sent and received over the transmission if we click on each 1st ICMP packet the above info is displayed
- the OSI model overview is displayed which layers are used at that specific time of transmission
- and the description of what happened at that time of transmission is displays in the bottom section
- we have outbound PDU details section in which we can see other header details in PDU format the type sequence number and data all those things
![[Pasted image 20240517080458.png]]

PDU -protocol data unit 
after simulation we can click on delete which is present below simulation mode option to delete 