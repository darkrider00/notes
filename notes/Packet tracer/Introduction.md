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
