## Overview

In this lab, you create several VPC networks and VM instances and test connectivity across networks. Specifically, you create two custom mode networks (**managementnet** and **privatenet**) with firewall rules and VM instances, as shown in this network diagram:

![vm-appliance virtual machine connected to two vm instances, and management and privatenet networks](https://cdn.qwiklabs.com/cczBwABQnb2t4cjbJ2gbDzcwAZ8dLDOZOtux5pz0YM4%3D)

The **mynetwork** network, its firewall rules, and two VM instances (**mynet-notus-vm** and **mynet-us-vm**) have already been created for you in this Qwiklabs project.

### Objectives

In this lab, you learn how to perform the following tasks:

- Create custom mode VPC networks with firewall rules
- Create VM instances using Compute Engine
- Explore the connectivity for VM instances across VPC networks
- Create a VM instance with multiple network interfaces

## Setup and requirements

For each lab, you get a new Google Cloud project and set of resources for a fixed time at no cost.

1. Click the **Start Lab** button. If you need to pay for the lab, a pop-up opens for you to select your payment method. On the left is the **Lab Details** panel with the following:
    
    - The **Open Google Cloud console** button
    - Time remaining
    - The temporary credentials that you must use for this lab
    - Other information, if needed, to step through this lab
2. Click **Open Google Cloud console** (or right-click and select **Open Link in Incognito Window** if you are running the Chrome browser).
    
    The lab spins up resources, and then opens another tab that shows the **Sign in** page.
    
    **_Tip:_** Arrange the tabs in separate windows, side-by-side.
    
    **Note:** If you see the **Choose an account** dialog, click **Use Another Account**.
    
3. If necessary, copy the **Username** below and paste it into the **Sign in** dialog.
    
    student-00-1b115f965e53@qwiklabs.net
    
    Copied!
    
    content_copy
    
    You can also find the **Username** in the **Lab Details** panel.
    
4. Click **Next**.
    
5. Copy the **Password** below and paste it into the **Welcome** dialog.
    
    83WYvlsISILk
    
    Copied!
    
    content_copy
    
    You can also find the **Password** in the **Lab Details** panel.
    
6. Click **Next**.
    
    **Important:** You must use the credentials the lab provides you. Do not use your Google Cloud account credentials.
    
    **Note:** Using your own Google Cloud account for this lab may incur extra charges.
    
7. Click through the subsequent pages:
    
    - Accept the terms and conditions.
    - Do not add recovery options or two-factor authentication (because this is a temporary account).
    - Do not sign up for free trials.

After a few moments, the Google Cloud console opens in this tab.

**Note:** To view a menu with a list of Google Cloud products and services, click the **Navigation menu** at the top-left, or type the service or product name in the **Search** field. ![Navigation menu icon](https://cdn.qwiklabs.com/9Fk8NYFp3quE9mF%2FilWF6%2FlXY9OUBi3UWtb2Ne4uXNU%3D)

## Task 1. Create custom mode VPC networks with firewall rules

Create two custom networks, **managementnet** and **privatenet**, along with firewall rules to allow **SSH**, **ICMP**, and **RDP** ingress traffic.

### Create the managementnet network

Create the **managementnet** network using the Cloud console.

1. In the Google Cloud console, in the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation menu")), click **VPC network** > **VPC networks**.  
    Notice the **default** and **mynetwork** networks with their subnets.
    
    Each Google Cloud project starts with the **default** network. In addition, the **mynetwork** network has been created for you as part of your network diagram.
    
2. Click **Create VPC Network**.
    
3. For **Name**, type **managementnet**.
    
4. For **Subnet creation mode**, click **Custom**.
    
5. For **New subnet**, specify the following, and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Name|managementsubnet-us|
    |Region|`us-east4`|
    |IPv4 range|10.130.0.0/20|
    
6. Click **Done**.
    
7. Click **EQUIVALENT COMMAND LINE**.
    
    These commands illustrate that networks and subnets can be created using the `gcloud` command line. You will create the **privatenet** network using these commands with similar parameters.
    
8. Click **Close**.
    
9. Click **Create**.
    

### Create the privatenet network

Create the **privatenet** network using the `gcloud` command line.

1. In the Cloud console, click **Activate Cloud Shell** (![Activate Cloud Shell icon](https://cdn.qwiklabs.com/ep8HmqYGdD%2FkUncAAYpV47OYoHwC8%2Bg0WK%2F8sidHquE%3D "Cloud Shell")).
2. If prompted, click **Continue**.
3. Run the following command to create the **privatenet** network:

gcloud compute networks create privatenet --subnet-mode=custom

Copied!

content_copy

4. Run the following command to create the **privatesubnet-us** subnet:

gcloud compute networks subnets create privatesubnet-us --network=privatenet --region=us-east4 --range=172.16.0.0/24

Copied!

content_copy

5. Run the following command to create the **privatesubnet-notus** subnet:

gcloud compute networks subnets create privatesubnet-notus --network=privatenet --region=europe-west1 --range=172.20.0.0/20

Copied!

content_copy

6. Run the following command to list the available VPC networks:

gcloud compute networks list

Copied!

content_copy

The output should look like this:

NAME: default
SUBNET_MODE: AUTO
BGP_ROUTING_MODE: REGIONAL
IPV4_RANGE:
GATEWAY_IPV4:

NAME: managementnet
SUBNET_MODE: CUSTOM
BGP_ROUTING_MODE: REGIONAL
IPV4_RANGE:
GATEWAY_IPV4:

NAME: mynetwork
SUBNET_MODE: AUTO
BGP_ROUTING_MODE: REGIONAL
IPV4_RANGE:
GATEWAY_IPV4:

NAME: privatenet
SUBNET_MODE: CUSTOM
BGP_ROUTING_MODE: REGIONAL
IPV4_RANGE:
GATEWAY_IPV4:

**Note:** **default** and **mynetwork** are auto mode networks and create subnets in each region automatically. **managementnet** and **privatenet** are custom mode networks and start with no subnets, which gives you full control over subnet creation.

7. Run the following command to list the available VPC subnets (sorted by VPC network):

gcloud compute networks subnets list --sort-by=NETWORK

Copied!

content_copy

The output should look like this:

NAME: default
REGION: northamerica-south1
NETWORK: default
RANGE: 10.224.0.0/20
STACK_TYPE: IPV4_ONLY
IPV6_ACCESS_TYPE: 
INTERNAL_IPV6_PREFIX: 
EXTERNAL_IPV6_PREFIX: 

NAME: default
REGION: europe-north2
NETWORK: default
RANGE: 10.226.0.0/20
STACK_TYPE: IPV4_ONLY
IPV6_ACCESS_TYPE: 
INTERNAL_IPV6_PREFIX: 
EXTERNAL_IPV6_PREFIX: 

NAME: managementsubnet-us
REGION: us-east1
NETWORK: managementnet
RANGE: 10.130.0.0/20
STACK_TYPE: IPV4_ONLY
IPV6_ACCESS_TYPE: 
INTERNAL_IPV6_PREFIX: 
EXTERNAL_IPV6_PREFIX: 

NAME: mynetwork
REGION: us-central1
NETWORK: mynetwork
RANGE: 10.128.0.0/20
STACK_TYPE: IPV4_ONLY
IPV6_ACCESS_TYPE: 
INTERNAL_IPV6_PREFIX: 
EXTERNAL_IPV6_PREFIX: 

NAME: mynetwork
REGION: europe-west1
NETWORK: mynetwork
RANGE: 10.132.0.0/20
STACK_TYPE: IPV4_ONLY
IPV6_ACCESS_TYPE: 
INTERNAL_IPV6_PREFIX: 
EXTERNAL_IPV6_PREFIX: 

NAME: mynetwork
REGION: us-west1
NETWORK: mynetwork
RANGE: 10.138.0.0/20
STACK_TYPE: IPV4_ONLY
IPV6_ACCESS_TYPE: 
INTERNAL_IPV6_PREFIX: 
EXTERNAL_IPV6_PREFIX: 

NAME: mynetwork
REGION: asia-east1
NETWORK: mynetwork
RANGE: 10.140.0.0/20
STACK_TYPE: IPV4_ONLY
IPV6_ACCESS_TYPE: 
INTERNAL_IPV6_PREFIX: 
EXTERNAL_IPV6_PREFIX: 

NAME: mynetwork
REGION: us-east1
NETWORK: mynetwork
RANGE: 10.142.0.0/20
STACK_TYPE: IPV4_ONLY
IPV6_ACCESS_TYPE: 
INTERNAL_IPV6_PREFIX: 
EXTERNAL_IPV6_PREFIX: 

NAME: mynetwork
REGION: asia-northeast1
NETWORK: mynetwork
RANGE: 10.146.0.0/20
STACK_TYPE: IPV4_ONLY
IPV6_ACCESS_TYPE: 
INTERNAL_IPV6_PREFIX: 
EXTERNAL_IPV6_PREFIX: 

NAME: mynetwork
REGION: asia-southeast1
NETWORK: mynetwork
RANGE: 10.148.0.0/20
STACK_TYPE: IPV4_ONLY
IPV6_ACCESS_TYPE: 
INTERNAL_IPV6_PREFIX: 
EXTERNAL_IPV6_PREFIX: 

NAME: mynetwork
REGION: us-east4
NETWORK: mynetwork
RANGE: 10.150.0.0/20
STACK_TYPE: IPV4_ONLY
IPV6_ACCESS_TYPE: 
INTERNAL_IPV6_PREFIX: 
EXTERNAL_IPV6_PREFIX: 

NAME: mynetwork
REGION: australia-southeast1
NETWORK: mynetwork
RANGE: 10.152.0.0/20
STACK_TYPE: IPV4_ONLY
IPV6_ACCESS_TYPE: 
INTERNAL_IPV6_PREFIX: 
EXTERNAL_IPV6_PREFIX:

**Note:** As expected, the **default** and **mynetwork** networks have subnets in [each region](https://cloud.google.com/compute/docs/regions-zones/#available), because they are auto mode networks. The **managementnet** and **privatenet** networks only have the subnets that you created, because they are custom mode networks.

8. In the Cloud console, in the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation menu")), click **VPC network** > **VPC networks**.  
    Verify that the same networks and subnets are listed in the Cloud console.

### Create the firewall rules for managementnet

Create firewall rules to allow **SSH**, **ICMP**, and **RDP** ingress traffic to VM instances on the **managementnet** network.

1. In the Cloud console, in the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation menu")), click **VPC network** > **Firewall**.
    
2. Click **Create Firewall Rule**.
    
3. Specify the following, and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Name|managementnet-allow-icmp-ssh-rdp|
    |Network|managementnet|
    |Targets|All instances in the network|
    |Source filter|IPv4 Ranges|
    |Source IPv4 ranges|0.0.0.0/0|
    |Protocols and ports|Specified protocols and ports|
    
4. For **tcp**, specify ports **22** and **3389**.
    
5. Click **Other protocols** and enter **icmp**.
    

**Note:** Make sure to include the **/0** in the **Source IPv4 ranges** to specify all networks.

6. Click **EQUIVALENT COMMAND LINE**.
    
    These commands illustrate that firewall rules can also be created using the `gcloud` command line. You will create the **privatenet**'s firewall rules using these commands with similar parameters.
    
7. Click **Close**.
    
8. Click **Create**.
    

### Create the firewall rules for privatenet

Create the firewall rules for **privatenet** network using the `gcloud` command line.

1. Return to **Cloud Shell**. If necessary, click **Activate Cloud Shell** (![Activate Cloud Shell icon](https://cdn.qwiklabs.com/ep8HmqYGdD%2FkUncAAYpV47OYoHwC8%2Bg0WK%2F8sidHquE%3D "Cloud Shell")).
2. Run the following command to create the **privatenet-allow-icmp-ssh-rdp** firewall rule:

gcloud compute firewall-rules create privatenet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=privatenet --action=ALLOW --rules=icmp,tcp:22,tcp:3389 --source-ranges=0.0.0.0/0

Copied!

content_copy

The output should look like this:

NAME: privatenet-allow-icmp-ssh-rdp
NETWORK: privatenet
DIRECTION: INGRESS
PRIORITY: 1000
ALLOW: icmp,tcp:22,tcp:3389
DENY:
DISABLED: False

3. Run the following command to list all the firewall rules (sorted by VPC network):

gcloud compute firewall-rules list --sort-by=NETWORK

Copied!

content_copy

The output should look like this:

NAME                              NETWORK        DIRECTION  PRIORITY  ALLOW                         DENY
default-allow-icmp                default        INGRESS    65534     icmp
default-allow-internal            default        INGRESS    65534     tcp:0-65535,udp:0-65535,icmp
default-allow-rdp                 default        INGRESS    65534     tcp:3389
default-allow-ssh                 default        INGRESS    65534     tcp:22
managementnet-allow-icmp-ssh-rdp  managementnet  INGRESS    1000      icmp,tcp:22,tcp:3389
mynetwork-allow-icmp              mynetwork      INGRESS    1000      icmp
mynetwork-allow-rdp               mynetwork      INGRESS    1000      tcp:3389
mynetwork-allow-ssh               mynetwork      INGRESS    1000      tcp:22
privatenet-allow-icmp-ssh-rdp     privatenet     INGRESS    1000      icmp,tcp:22,tcp:3389

The firewall rules for **mynetwork** network have been created for you. You can define multiple protocols and ports in one firewall rule (**privatenet** and **managementnet**) or spread them across multiple rules (**default** and **mynetwork**).

4. In the Cloud console, on the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation menu")), click **VPC network** > **Firewall**.  
    Verify that the same firewall rules are listed in the Cloud console.

Click _Check my progress_ to verify the objective.

Create custom mode VPC networks with firewall rules

Check my progress

## Task 2. Create VM instances

Create two VM instances:

- **managementnet-us-vm** in **managementsubnet-us**
- **privatenet-us-vm** in **privatesubnet-us**

### Create the managementnet-us-vm instance

Create the **managementnet-us-vm** instance using the Cloud console.

1. In the Cloud console, in the **Navigation menu** (![Navigation menu](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation menu")), click **Compute Engine** > **VM instances**.
    
    **mynet-us-vm** and **mynet-notus-vm** have been created for you as part of your network diagram.
    
2. Click **Create Instance**.
    
3. Specify the following, and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Name|managementnet-us-vm|
    |Region|`us-east4`|
    |Zone|`us-east4-a`|
    
4. In the left frame, click **Machine configuration**. Make sure the following values are selected: | Series | E2| | Machine type | 2vCPU (4 GB memory, e2-medium)|
    
5. In the left frame, click **Networking**.
    
6. For **Network interfaces**, click the dropdown icon to edit.
    
7. Specify the following, and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Network|managementnet|
    |Subnetwork|managementsubnet-us|
    

**Note:** The subnets available for selection are restricted to those in the selected region.

8. Click **Done**.
    
9. Click **Equivalent Code**.
    
    This illustrates that VM instances can also be created using the `gcloud` command line. You will create the **privatenet-us-vm** instance using these commands with similar parameters.
    
10. Click **Toggle panel "Equivalent code"**.
    
11. Click **Create**.
    

### Create the privatenet-us-vm instance

Create the **privatenet-us-vm** instance using the `gcloud` command line.

1. Return to **Cloud Shell**. If necessary, click **Activate Cloud Shell** (![Activate Cloud Shell icon](https://cdn.qwiklabs.com/ep8HmqYGdD%2FkUncAAYpV47OYoHwC8%2Bg0WK%2F8sidHquE%3D "Cloud Shell")).
2. Run the following command to create the **privatenet-us-vm** instance:

gcloud compute instances create privatenet-us-vm --zone=us-east4-a --machine-type=e2-medium --subnet=privatesubnet-us

Copied!

content_copy

The output should look like this:

NAME: privatenet-us-vm
ZONE: us-east4-a
MACHINE_TYPE: e2-medium
PREEMPTIBLE:
INTERNAL_IP: 172.16.0.2
EXTERNAL_IP: 34.70.73.27
STATUS: RUNNING

3. Run the following command to list all the VM instances (sorted by zone):

gcloud compute instances list --sort-by=ZONE

Copied!

content_copy

The output should look like this:

NAME                 ZONE            MACHINE_TYPE   PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP     STATUS
mynet-notus-vm          europe-west1-c  e2-medium               10.132.0.2   35.205.124.164  RUNNING
managementnet-us-vm  us-east4-a   e2-medium               10.130.0.2   35.226.20.87    RUNNING
mynet-us-vm          us-east4-a   e2-medium               10.128.0.2   35.232.252.86   RUNNING
privatenet-us-vm     us-east4-a   e2-medium               172.16.0.2   35.184.221.40   RUNNING

4. In the Cloud console, in the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation menu")), click **Compute Engine** > **VM instances**.  
    Verify that the VM instances are listed in the Cloud console.
    
5. For **Columns**, select **Network**.
    
    There are three instances in the US and one instance that is not in the US. These instances are spread across three VPC networks (**managementnet**, **mynetwork**, and **privatenet**), with no instance in the same zone and network as another. In the next task, you explore the effect this has on internal connectivity.
    

Click _Check my progress_ to verify the objective.

Create VM instances

Check my progress

## Task 3. Explore the connectivity between VM instances

Explore the connectivity between the VM instances. Specifically, determine the effect of having VM instances in the same zone versus having instances in the same VPC network.

### Ping the external IP addresses

Ping the external IP addresses of the VM instances to determine whether you can reach the instances from the public internet.

1. In the Cloud console, in the **Navigation menu**, click **Compute Engine** > **VM instances**.  
    Note the external IP addresses for **mynet-notus-vm**, **managementnet-us-vm**, and **privatenet-us-vm**.
2. For **mynet-us-vm**, click **SSH** to launch a terminal and connect.
3. To test connectivity to **mynet-notus-vm**'s external IP, run the following command, replacing **mynet-notus-vm**'s external IP:

ping -c 3 <Enter mynet-notus-vm's external IP here>

Copied!

content_copy

This should work!

4. To test connectivity to **managementnet-us-vm**'s external IP, run the following command, replacing **managementnet-us-vm**'s external IP:

ping -c 3 <Enter managementnet-us-vm's external IP here>

Copied!

content_copy

This should work!

5. To test connectivity to **privatenet-us-vm**'s external IP, run the following command, replacing **privatenet-us-vm**'s external IP:

ping -c 3 <Enter privatenet-us-vm's external IP here>

Copied!

content_copy

This should work!

**Note:** You can ping the external IP address of all VM instances, even though they are in either a different zone or VPC network. This confirms that public access to those instances is only controlled by the **ICMP** firewall rules that you established earlier.

### Ping the internal IP addresses

Ping the internal IP addresses of the VM instances to determine whether you can reach the instances from within a VPC network.

Which instance(s) should you be able to ping from mynet-us-vm using internal IP addresses?

privatenet-us-vm

managementnet-us-vm

mynet-notus-vm

Submit

1. In the Cloud console, in the **Navigation menu**, click **Compute Engine** > **VM instances**.  
    Note the internal IP addresses for **mynet-notus-vm**, **managementnet-us-vm**, and **privatenet-us-vm**.
2. Return to the **SSH** terminal for **mynet-us-vm**.
3. To test connectivity to **mynet-notus-vm**'s internal IP, run the following command, replacing **mynet-notus-vm**'s internal IP:

ping -c 3 <Enter mynet-notus-vm's internal IP here>

Copied!

content_copy

**Note:** You can ping the internal IP address of **mynet-notus-vm** because it is on the same VPC network as the source of the ping (**mynet-us-vm**), even though both VM instances are in separate zones, regions, and continents!

4. To test connectivity to **managementnet-us-vm**'s internal IP, run the following command, replacing **managementnet-us-vm**'s internal IP:

ping -c 3 <Enter managementnet-us-vm's internal IP here>

Copied!

content_copy

**Note:** This should not work, as indicated by a 100% packet loss!

5. To test connectivity to **privatenet-us-vm**'s internal IP, run the following command, replacing **privatenet-us-vm**'s internal IP:

ping -c 3 <Enter privatenet-us-vm's internal IP here>

Copied!

content_copy

**Note:** This should not work either, as indicated by a 100% packet loss! You cannot ping the internal IP address of **managementnet-us-vm** and **privatenet-us-vm** because they are in separate VPC networks from the source of the ping (**mynet-us-vm**), even though they are all in the same zone.

VPC networks are by default isolated private networking domains. However, no internal IP address communication is allowed between networks, unless you set up mechanisms such as VPC peering or VPN.

## Task 4. Create a VM instance with multiple network interfaces

Every instance in a VPC network has a default network interface. You can create additional network interfaces attached to your VMs. Multiple network interfaces enable you to create configurations in which an instance connects directly to several VPC networks (up to 8 interfaces, depending on the instance's type).

### Create the VM instance with multiple network interfaces

Create the **vm-appliance** instance with network interfaces in **privatesubnet-us**, **managementsubnet-us**, and **mynetwork**. The CIDR ranges of these subnets do not overlap, which is a requirement for creating a VM with multiple network interface controllers (NICs).

1. In the Cloud console, in the **Navigation menu**, click **Compute Engine** > **VM instances**.
    
2. Click **Create Instance**.
    
3. Specify the following, and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Name|vm-appliance|
    |Region|`us-east4`|
    |Zone|`us-east4-a`|
    
4. In the left frame, click **Machine configuration**.
    
5. Make sure that the following values are selected. | Series | E2| | Machine type | 4vCPUs (16 GB memory, e2-standard-4)|
    

**Note:** The number of interfaces allowed in an instance is dependent on the instance's machine type and the number of vCPUs. The e2-standard-4 allows up to 4 network interfaces. Learn more about determining the number allowed interfaces from the [Creating instances with multiple network interfaces guide](https://cloud.google.com/vpc/docs/create-use-multiple-interfaces#max-interfaces).

6. In the left frame, click **Networking**.
    
7. For **Network interfaces**, click the dropdown icon to edit.
    
8. Specify the following, and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Network|privatenet|
    |Subnetwork|privatesubnet-us|
    
9. Click **Done**.
    
10. Click **Add a network interface**.
    
11. Specify the following, and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Network|managementnet|
    |Subnetwork|managementsubnet-us|
    
12. Click **Done**.
    
13. Click **Add a network interface**.
    
14. Specify the following, and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Network|mynetwork|
    |Subnetwork|mynetwork|
    
15. Click **Done**.
    
16. Click **Create**.
    

### Explore the network interface details

Explore the network interface details of **vm-appliance** within the Cloud console and within the VM's terminal.

1. In the Cloud console, in the **Navigation menu**, click **Compute Engine** > **VM instances**.
2. To open the **Network interface details** page, in the **Internal IP** address of **vm-appliance**, click **nic0**.
3. Verify that **nic0** is attached to **privatesubnet-us**, is assigned an internal IP address within that subnet (172.16.0.0/24), and has applicable firewall rules.
4. Click **nic0** and select **nic1**.
5. Verify that **nic1** is attached to **managementsubnet-us**, is assigned an internal IP address within that subnet (10.130.0.0/20), and has applicable firewall rules.
6. Click **nic1** and select **nic2**.
7. Verify that **nic2** is attached to **mynetwork**, is assigned an internal IP address within that subnet (10.128.0.0/20), and has applicable firewall rules.

**Note:** Each network interface has its own internal IP address so that the VM instance can communicate with those networks.

8. In the Cloud console, in the **Navigation menu**, click **Compute Engine** > **VM instances**.
9. For **vm-appliance**, click **SSH** to launch a terminal and connect.
10. Run the following command to list the network interfaces within the VM instance:

sudo ifconfig

Copied!

content_copy

The output should look like this:

ens4: flags=4163<up>  mtu 1460
        inet 172.16.0.3  netmask 255.255.255.255  broadcast 0.0.0.0
        inet6 fe80::4001:acff:fe10:3  prefixlen 64  scopeid 0x20<link>
        ether 42:01:ac:10:00:03  txqueuelen 1000  (Ethernet)
        RX packets 99  bytes 24688 (24.1 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 109  bytes 20015 (19.5 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

ens5: flags=4163<up>  mtu 1460
        inet 10.130.0.3  netmask 255.255.255.255  broadcast 0.0.0.0
        inet6 fe80::4001:aff:fe82:3  prefixlen 64  scopeid 0x20<link>
        ether 42:01:0a:82:00:03  txqueuelen 1000  (Ethernet)
        RX packets 585  bytes 137966 (134.7 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 566  bytes 52713 (51.4 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

ens6: flags=4163<up>  mtu 1460
        inet 10.142.0.3  netmask 255.255.255.255  broadcast 0.0.0.0
        inet6 fe80::4001:aff:fe8e:3  prefixlen 64  scopeid 0x20<link>
        ether 42:01:0a:8e:00:03  txqueuelen 1000  (Ethernet)
        RX packets 19  bytes 4182 (4.0 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 36  bytes 3615 (3.5 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<up>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 8  bytes 868 (868.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 8  bytes 868 (868.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
</host></up></up></up></up>

**Note:** The **sudo ifconfig** command lists a Linux VM's network interfaces with the internal IP addresses for each interface.

### Explore the network interface connectivity

Demonstrate that the **vm-appliance** instance is connected to **privatesubnet-us**, **managementsubnet-us**, and **mynetwork** by pinging VM instances on those subnets.

Which instance(s) should you be able to ping from vm-appliance using internal IP addresses?

mynet-notus-vm

managementnet-us-vm

mynet-us-vm

privatenet-us-vm

Submit

1. In the Cloud console, in the **Navigation menu**, click **Compute Engine** > **VM instances**.
2. Note the internal IP addresses for **privatenet-us-vm**, **managementnet-us-vm**, **mynet-us-vm**, and **mynet-notus-vm**.
3. Return to the **SSH** terminal for **vm-appliance**.
4. To test connectivity to **privatenet-us-vm**'s internal IP, run the following command, replacing **privatenet-us-vm**'s internal IP:

ping -c 3 <Enter privatenet-us-vm's internal IP here>

Copied!

content_copy

This works!

5. Repeat the same test by running the following:

ping -c 3 privatenet-us-vm

Copied!

content_copy

**Note:** You can ping **privatenet-us-vm** by its name because VPC networks have an internal DNS service that allows you to address instances by their DNS names instead of their internal IP addresses. When an internal DNS query is made with the instance hostname, it resolves to the primary interface (nic0) of the instance. Therefore, this only works for **privatenet-us-vm** in this case.

6. To test connectivity to **managementnet-us-vm**'s internal IP, run the following command, replacing **managementnet-us-vm**'s internal IP:

ping -c 3 <Enter managementnet-us-vm's internal IP here>

Copied!

content_copy

This works!

7. To test connectivity to **mynet-us-vm**'s internal IP, run the following command, replacing **mynet-us-vm**'s internal IP:

ping -c 3 <Enter mynet-us-vm's internal IP here>

Copied!

content_copy

This works!

8. To test connectivity to **mynet-notus-vm**'s internal IP, run the following command, replacing **mynet-notus-vm**'s internal IP:

ping -c 3 <Enter mynet-notus-vm's internal IP here>

Copied!

content_copy

**Note:** This does not work! In a multiple interface instance, every interface gets a route for the subnet that it is in. In addition, the instance gets a single default route that is associated with the primary interface ens4. Unless manually configured otherwise, any traffic leaving an instance for any destination other than a directly connected subnet will leave the instance via the default route on ens4.

9. To list the routes for **vm-appliance** instance, run the following command:

ip route

Copied!

content_copy

The output should look like this example:

default via 172.16.0.1 dev ens4 proto dhcp src 172.16.0.3 metric 100
10.130.0.0/20 via 10.130.0.1 dev ens5
10.130.0.0/20 via 10.130.0.1 dev ens5 proto dhcp src 10.130.0.3 metric 100
10.130.0.1 dev ens5 scope link
10.130.0.1 dev ens5 proto dhcp scope link src 10.130.0.3 metric 100
10.142.0.0/20 via 10.142.0.1 dev ens6
10.142.0.0/20 via 10.142.0.1 dev ens6 proto dhcp src 10.142.0.3 metric 100
10.142.0.1 dev ens6 scope link
10.142.0.1 dev ens6 proto dhcp scope link src 10.142.0.3 metric 100
169.254.169.254 dev ens5 proto dhcp scope link src 10.130.0.3 metric 100
169.254.169.254 dev ens6 proto dhcp scope link src 10.142.0.3 metric 100
169.254.169.254 via 172.16.0.1 dev ens4 proto dhcp src 172.16.0.3 metric 100
172.16.0.0/24 via 172.16.0.1 dev ens4 proto dhcp src 172.16.0.3 metric 100
172.16.0.1 dev ens4 proto dhcp scope link src 172.16.0.3 metric 100

**Note:** The primary interface ens4 gets the default route (default via 172.16.0.1 dev ens4), and all three interfaces, ens4, ens5, and ens6, get routes for their respective subnets. Because the subnet of **mynet-notus-vm** (**10.132.0.0/20**) is not included in this routing table, the ping to that instance leaves **vm-appliance** on ens4 (which is on a different VPC network).

Learn more about how you can change this behavior by configuring policy routing from the [Creating instances with multiple network interfaces guide](https://cloud.google.com/vpc/docs/create-use-multiple-interfaces#configuring_policy_routing).

Click _Check my progress_ to verify the objective.

Create the VM instance with multiple network interfaces

Check my progress

## Review

In this lab, you created several custom mode VPC networks, firewall rules, and VM instances using the Cloud Console and the gcloud command line. Then you tested the connectivity across VPC networks, which worked when pinging external IP addresses but not when pinging internal IP addresses. Thus you created a VM instance with three network interfaces and verified internal connectivity for VM instances that are on the subnets that are attached to the multiple interface VM.

## End your lab

When you have completed your lab, click **End Lab**. Google Cloud Skills Boost removes the resources you’ve used and cleans the account for you.