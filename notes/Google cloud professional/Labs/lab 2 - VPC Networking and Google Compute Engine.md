
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
    
    student-04-28c9abf03068@qwiklabs.net
    
    Copied!
    
    content_copy
    
    You can also find the **Username** in the **Lab Details** panel.
    
4. Click **Next**.
    
5. Copy the **Password** below and paste it into the **Welcome** dialog.
    
    wuCr4IJvoa37
    
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

## Task 1. Explore the default network

Each Google Cloud project has a **default** network with subnets, routes, and firewall rules.

### View the subnets

The **default** network has a subnet in [each Google Cloud region](https://cloud.google.com/compute/docs/regions-zones/#available).

1. In the Cloud Console, on the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **VPC network** > **VPC networks**.
    
2. Click **default**.
    
3. Click **Subnets**.
    

Notice the **default** network with its subnets.  
Each subnet is associated with a Google Cloud region and a private RFC 1918 CIDR block for its internal **IP addresses range** and a **gateway**.

### View the routes

Routes tell VM instances and the VPC network how to send traffic from an instance to a destination, either inside the network or outside Google Cloud. Each VPC network comes with some default routes to route traffic among its subnets and send traffic from eligible instances to the internet.

1. In the left pane, click **Routes**.
    
2. In **Effective Routes** click **Network**, and then select **default**.
    
3. Click **Region** and select the Lab Region assigned to you by Qwiklabs.
    
4. Click **View**.
    
    Notice that there is a route for each subnet.  
    These routes are managed for you, but you can create custom static routes to direct some packets to specific destinations. For example, you can create a route that sends all outbound traffic to an instance configured as a NAT gateway.
    

### View the Firewall rules

Each VPC network implements a distributed virtual firewall that you can configure. Firewall rules allow you to control which packets are allowed to travel to which destinations. Every VPC network has two implied firewall rules that block all incoming connections and allow all outgoing connections.

- In the left pane, click **Firewall**.  
    Notice that there are 4 **Ingress** firewall rules for the **default** network:
    - default-allow-icmp
    - default-allow-rdp
    - default-allow-ssh
    - default-allow-internal

**Note:** These firewall rules allow **ICMP**, **RDP**, and **SSH** ingress traffic from anywhere (0.0.0.0/0) and all **TCP**, **UDP**, and **ICMP** traffic within the network (10.128.0.0/9). The **Targets**, **Filters**, **Protocols/ports**, and **Action** columns explain these rules.

### Delete the Firewall rules

1. Select all of the default network firewall rules.
2. Click **Delete**.
3. Click **Delete** to confirm the deletion of the firewall rules.

### Delete the default network

1. In the Cloud Console, on the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **VPC network** > **VPC networks**.
2. Select the **default** network.
3. Click **Delete VPC network**.
4. Click **Delete** to confirm the deletion of the **default** network.  
    Wait for the network to be deleted before continuing.
5. In the left pane, click **Routes**.  
    Notice that there are no routes.
6. In the left pane, click **Firewall**.  
    Notice that there are no firewall rules.

**Note:** Without a VPC network, there are no routes and no firewall rules!

### Try to create a VM instance

Verify that you cannot create a VM instance without a VPC network.

1. On the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **Compute Engine** > **VM instances**.
2. Click **Create instance**.
3. Accept the default values and click **Create**. An error is shown on the **Networking** tab.
4. Click **Go to Issues**.
5. In **Network Interfaces**, notice the no more networks and no network available errors.
6. Click **Cancel**.

**Note:** As expected, you cannot create a VM instance without a VPC network!

## Task 2. Create a VPC network and VM instances

Create a VPC network so that you can create VM instances.

### Create an auto mode VPC network with Firewall rules

Replicate the **default** network by creating an auto mode network.

1. On the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **VPC network** > **VPC networks**.
2. Click **Create VPC network**.
3. For **Name**, type **mynetwork**.
4. For **Subnet creation mode**, click **Automatic**. Auto mode networks create subnets in each region automatically.
5. For **Firewall rules**, select all available rules. These are the same standard firewall rules that the default network had. The **deny-all-ingress** and **allow-all-egress** rules are also displayed, but you cannot check or uncheck them because they are implied. These two rules have a lower **Priority** (higher integers indicate lower priorities) so that the allow ICMP, custom, RDP and SSH rules are considered first.
6. Click **Create**. When the new network is ready, notice that a subnet was created for each region.
7. Explore the IP address range for the subnets in `us-east4` and `asia-east1`.

**Note:** If you ever delete the default network, you can quickly re-create it by creating an auto mode network as you just did. After recreating the network, allow-internal changes to allow-custom firewall rule.

### **Create a VM instance in `us-east4`**

Create a VM instance in the `us-east4` region. Selecting a region and zone determines the subnet and assigns the internal IP address from the subnet's IP address range.

1. On the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **Compute Engine** > **VM instances**.
    
2. Click **Create Instance**.
    
3. Specify the following:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Name|mynet-us-vm|
    |Region|`us-east4`|
    |Zone|`us-east4-b`|
    
4. For **Series**, select **E2**.
    
5. For **Machine type**, select **e2-micro (2 vCPU, 1 GB memory)**.
    
6. Click **Create**.
    

### Create a VM instance in `asia-east1`

Create a VM instance in the `asia-east1` region.

1. Click **Create Instance**.
    
2. Specify the following, and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Name|mynet-r2-vm|
    |Region|`asia-east1`|
    |Zone|`asia-east1-c`|
    
3. For **Series**, select **E2**.
    
4. For **Machine type**, select **e2-micro (2 vCPU, 1 GB memory)**.
    
5. Click **Create**.
    

**Note:** The **External IP addresses** for both VM instances are ephemeral. If an instance is stopped, any ephemeral external IP addresses assigned to the instance are released back into the general Compute Engine pool and become available for use by other projects.

When a stopped instance is started again, a new ephemeral external IP address is assigned to the instance. Alternatively, you can reserve a static external IP address, which assigns the address to your project indefinitely until you explicitly release it.

Click _Check my progress_ to verify the objective.

Create a VPC network and VM instance

Check my progress

## Task 3. Explore the connectivity for VM instances

Explore the connectivity for the VM instances. Specifically, try to SSH to your VM instances using tcp:22, and ping both the internal and external IP addresses of your VM instances using ICMP. Then explore the effects of the firewall rules on connectivity by removing the firewall rules individually.

### Verify connectivity for the VM instances

The firewall rules that you created with **mynetwork** allow ingress SSH and ICMP traffic from within **mynetwork** (internal IP) and outside that network (external IP).

1. On the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **Compute Engine** > **VM instances**.  
    Note the external and internal IP addresses for **mynet-r2-vm**.
    
2. For **mynet-us-vm**, click **SSH** to launch a terminal and connect.
    
3. If an **Authorize** popup appears, click on **Authorize**
    

**Note:** You can SSH because of the **allow-ssh** firewall rule, which allows incoming traffic from anywhere (0.0.0.0/0) for **tcp:22**. The SSH connection works seamlessly because Compute Engine generates an SSH key for you and stores it in one of the following locations:

- By default, Compute Engine adds the generated key to project or instance metadata.
- If your account is configured to use OS Login, Compute Engine stores the generated key with your user account.

Alternatively, you can control access to Linux instances by creating SSH keys and editing public SSH key metadata.

3. To test connectivity to **mynet-r2-vm**'s internal IP, run the following command, replacing **mynet-r2-vm**'s internal IP:

ping -c 3 <Enter mynet-r2-vm's internal IP here>

Copied!

content_copy

You can ping **mynet-r2-vm**'s internal IP because of the **allow-custom** firewall rule.

4. To test connectivity to **mynet-r2-vm**'s external IP, run the following command, replacing **mynet-r2-vm**'s external IP:

ping -c 3 <Enter mynet-r2-vm's external IP here>

Copied!

content_copy

Which firewall rule allows the ping to mynet-r2-vm's external IP address?

mynetwork-allow-icmp

mynetwork-allow-rdp

mynetwork-allow-custom

mynetwork-allow-ssh

Submit

**Note:** You can SSH to **mynet-us-vm** and ping **mynet-r2-vm**'s internal and external IP address as expected. Alternatively, you can SSH to **mynet-r2-vm** and ping **mynet-us-vm**'s internal and external IP address, which also works.

### Remove the allow-icmp firewall rules

Remove the **allow-icmp** firewall rule and try to ping the internal and external IP address of **mynet-r2-vm**.

1. On the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **VPC network** > **Firewall**.
    
2. Select the **mynetwork-allow-icmp** rule.
    
3. Click **Delete**.
    
4. Click **Delete** to confirm the deletion.  
    Wait for the firewall rule to be deleted.
    
5. Return to the **mynet-us-vm** SSH terminal.
    
6. To test connectivity to **mynet-r2-vm**'s internal IP, run the following command, replacing **mynet-r2-vm**'s internal IP:
    

ping -c 3 <Enter mynet-r2-vm's internal IP here>

Copied!

content_copy

You can ping **mynet-r2-vm**'s internal IP because of the **allow-custom** firewall rule.

7. To test connectivity to **mynet-r2-vm**'s external IP, run the following command, replacing **mynet-r2-vm**'s external IP:

ping -c 3 <Enter mynet-r2-vm's external IP here>

Copied!

content_copy

**Note:** The **100% packet loss** indicates that you cannot ping **mynet-r2-vm**'s external IP. This is expected because you deleted the **allow-icmp** firewall rule!

### Remove the allow-custom firewall rules

Remove the **allow-custom** firewall rule and try to ping the internal IP address of **mynet-r2-vm**.

1. On the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **VPC network** > **Firewall**.
2. Select the **mynetwork-allow-custom** rule.
3. Click **Delete**.
4. Click **Delete** to confirm the deletion.  
    Wait for the firewall rule to be deleted.
5. Return to the **mynet-us-vm** SSH terminal.
6. To test connectivity to **mynet-r2-vm**'s internal IP, run the following command, replacing **mynet-r2-vm**'s internal IP:

ping -c 3 <Enter mynet-r2-vm's internal IP here>

Copied!

content_copy

**Note:** The **100% packet loss** indicates that you cannot ping **mynet-r2-vm**'s internal IP. This is expected because you deleted the **allow-custom** firewall rule!

7. Close the SSH terminal:

exit

Copied!

content_copy

### Remove the allow-ssh firewall rules

Remove the **allow-ssh** firewall rule and try to SSH to **mynet-us-vm**.

1. On the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation menu")), click **VPC network** > **Firewall**.
2. Select the **mynetwork-allow-ssh** rule.
3. Click **Delete**.
4. Click **Delete** to confirm the deletion.
5. Wait for the firewall rule to be deleted.
6. On the **Navigation menu**, click **Compute Engine** > **VM instances**.
7. For **mynet-us-vm**, click **SSH** to launch a terminal and connect.

**Note:** The **Connection failed** message indicates that you cannot SSH to **mynet-us-vm** because you deleted the **allow-ssh** firewall rule!

## Task 4. Review

In this lab, you explored the default network along with its subnets, routes, and firewall rules. You deleted the default network and determined that you cannot create any VM instances without a VPC network.

Thus, you created a new auto mode VPC network with subnets, routes, firewall rules, and two VM instances. Then you tested the connectivity for the VM instances and explored the effects of the firewall rules on connectivity.

End your lab


login with details 

![[Pasted image 20250314175603.png]]

click on that 

![[Pasted image 20250314175632.png]]

click on default 

![[Pasted image 20250314175654.png]]

Each subnet is associated with a Google Cloud region and a private RFC 1918 CIDR block for its internal **IP addresses range** and a **gateway**.

RFC:
describe the Internet's technical foundations, such as addressing, routing, and transport technologies.
https://www.youtube.com/watch?v=8IXLpoN8Xj0

![[Pasted image 20250314175909.png]]

