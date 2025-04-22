## Overview

In this lab, you design and implement a classic hub-and-spoke network topology. Your pre-configured environment includes three VPC networks—a central hub and two branches (spoke1 and spoke2). You will create virtual machines (VMs) on each network to test connectivity.

You begin by verifying connectivity between the VMs within and across VPCs. Then, you use NCC to implement a hub and spoke. You retest connectivity to confirm that your hub-and-spoke architecture is fully functional.

### Objectives

In this lab, you learn how to perform the following tasks:

- Configure VMs in different VPCs.
- Test connectivity between networks before implementing a hub and spoke.
- Use NCC to create a hub and spoke.
- Test connectivity after implementing a hub and spoke.
- Use Network Topology to view metrics for traffic between entities.

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
    
    student-04-eb9be70d5af5@qwiklabs.net
    
    Copied!
    
    content_copy
    
    You can also find the **Username** in the **Lab Details** panel.
    
4. Click **Next**.
    
5. Copy the **Password** below and paste it into the **Welcome** dialog.
    
    rA3UB4670PNv
    
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

## Task 1. Explore the pre-configured network

The network **hub-vpc** with **hub-subnet**, **spoke1-vpc** with **spoke1-subnet**, and **spoke2-vpc** with **spoke2-subnet** along with firewall rules for **RDP**, **SSH**, and **ICMP** traffic have been configured for you.

- In the Google Cloud console, in the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **VPC network > VPC networks**.  
    Notice the **hub-vpc**, **spoke1-vpc**, and **spoke2-vpc** network with its subnets: **hub-subnet**, **spoke1-subnet**, and **spoke2-subnet**.
    
    Each Google Cloud project starts with the **default** network. In addition, the **hub-vpc**, **spoke1-vpc**, and **spoke2-vpc** network has been created for you as part of your network diagram.
    
    You create a VM in **hub-subnet**, **spoke1-subnet**, and **spoke2-subnet**.
    

### Explore the firewall rules

1. On the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **VPC network > Firewall**.  
    Notice the **app-allow-icmp** and **app-allow-ssh-rdp** firewall rules.
    
    These firewall rules have been created for you.
    

## Task 2. Create a VM in each VPC

1. On the **Navigation menu**, click **Compute Engine > VM instances**.
2. Click **Create Instance**.
3. Specify **Name** as **hub-vm**.
4. In the left frame, click **Networking**.
5. Under **Network interfaces** , click **default**. From the **Network** dropdown select **hub-vpc**.
6. Click **Create**.

Repeat the process to create a **spoke1-vm** VM in `spoke1-vpc` and a **spoke2-vm** VM in `spoke2-vpc`.

Click **Check my progress** to verify the objective.

Create a VM in each VPC

Check my progress

## Task 3: Test connectivity

spoke1-vm and spoke2-vm are in two different VPCs. Let us test the connectivity between the two.

1. On the **VM instances** page, for **spoke1-vm**, copy the internal IP address.
2. On the **VM instances** page, for **spoke2-vm**, click **SSH**.
3. Run the following command:

ping <internal IP address of spoke1-vm>

Copied!

content_copy

Notice how the ping fails. This should execute and display 100% packet loss. Press **Ctrl+C** to stop the command.

3. Now, SSH into **spoke1-vm** to test the connectivity from **spoke1-vm** to **spoke2-vm**:

ping <internal IP address of spoke2-vm>

Copied!

content_copy

Notice how the ping fails. This should execute and display 100% packet loss. Press **Ctrl+C** to stop the command.

## Task 4: Create a hub and spoke using NCC

Network Connectivity Center lets you create VPC spokes to connect VPC networks together for full mesh connectivity.

1. On the Google Cloud console title bar, type **Network Connectivity Center** in the Search field, then click **Network Connectivity Center** in the **Products & Page** section.
2. Click **Create hub**.
3. Enter **my-hub** for **Hub Name**.
4. Click **Next step**.
5. Click **Add a spoke**.
6. Enter **spoke1** for first **Spoke Name**.
7. Select **VPC network** as the Spoke type.
8. To add a VPC network to the spoke, select **spoke1-vpc**.
9. Click Done.
10. Click **Add a spoke** to add a second spoke,
11. Enter **spoke2** for second **Spoke Name**.
12. Select VPC network as the Spoke type.
13. Choose **spoke2-vpc** as the VPC network for this spoke.
14. Click Done.
15. When you have finished adding spokes, click **Create**.

Click **Check my progress** to verify the objective.

Create a hub and spoke using NCC

Check my progress

## Task 5. Retest connectivity

VPC spokes reduce the operational complexity of managing the individual pair-wise VPC Network Peering connections through the use of VPC spokes and a centralized connectivity management model. Now you retest the connectivity between the VMs from spokes.

This task has been performed for you at the start of this lab. You will need to SSH into VM and run the following command to setup the environment.

1. On the **Navigation** menu, click **Compute Engine > VM instances**.
    
2. Select the SSH button next to **spoke1-vm** to SSH into the VM.
    
3. If prompted "Allow SSH-in-browser to connect to VMs," click **Authorize**.
    
4. Run the following command:
    

ping -c 3 <internal IP address of spoke2-vm>

Copied!

content_copy

5. Repeat the previous steps for **spoke2-vm**.

## Task 6. Explore the Network Topology Tool

Network Topology is a visualization tool that shows the topology of your network infrastructure. You can also view metrics and details of network traffic to other Shared VPC networks and inter-region traffic.

For each Network Topology hierarchy, the Google Cloud console displays a single metric for Compute Engine virtual machine (VM) instance entities and region entities, as well as for connections.

1. On the Google Cloud console title bar, type **Network Topology** in the Search field, then click **Network Topology** in the **Products & Page** section.
2. Hover over an entity to display the **Expand** icon for expanding or **Collapse** icon for collapsing.
3. In the Metrics and insights section, select an insight from the options.


