

## Overview

Google Cloud load balancers offer traffic management capabilities that vary by load balancer.

In this lab, you create a regional internal Application Load Balancer with two backends. Each backend will be an instance group. You will configure the load balancer to create a blue-green deployment.

The blue deployment refers to the current version of your application, and the green deployment refers to a new application version. You configure the load balancer to send 70% of the traffic to the blue deployment and 30% to the green deployment. When you’re finished, the environment will look like this:

![The image shows a VPC network with two subnets, each with a managed instance group. One subnet is used for the blue deployment, and the other is used for the green deploynment. Client traffic to the subnets is handled by the load balancer.](https://cdn.qwiklabs.com/FgrZkcSEqghVxKV14KPVgNzTUMo0lQfmqTgpG45%2BTYA%3D)

## Objectives

In this lab, you perform the following tasks:

- View the Google Cloud infrastructure that the load balancer will use.
- Create a regional internal Application Load Balancer with two backends.
- Implement traffic management on the load balancer.
- Test the load balancer.

## Setup

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
    
    student-04-2ba4c568a75c@qwiklabs.net
    
    Copied!
    
    content_copy
    
    You can also find the **Username** in the **Lab Details** panel.
    
4. Click **Next**.
    
5. Copy the **Password** below and paste it into the **Welcome** dialog.
    
    JWtatNKVBl5t
    
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

## Task 1. View the Google Cloud infrastructure that the load balancer will use

In this task, you explore the pre-configured Google Cloud infrastructure, including the network, firewall rules, and instance groups, that the load balancer will utilize. You then create a test VM and verify the backend instances.

1. In the Google Cloud console, in the **Navigation menu** (![Navigation menu](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation menu")), click **VPC network > VPC networks**.
    
    Each Google Cloud project starts with the _default_ network. In addition, the _my-internal-app_ network was created for you as part of your network diagram.
    
    Note the _my-internal-app_ network with its subnets: _subnet-a_ and _subnet-b_. Both subnets are in the `us-central1` region.
    
    Managed instance groups in _subnet-a_ and _subnet-b_ were also created for you.
    
2. (Optional) Click **subnet-a** and observe its configuration.
    
3. (Optional) Click **subnet-b** and observe its configuration.
    
4. In the **Navigation menu** (![Navigation menu](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation menu")), click **VPC network > Firewall**.  
    Note the following firewall rules that were created for you:
    
    |Firewall rule|Purpose|
    |---|---|
    |app-allow-icmp|Allows ICMP communication|
    |app-allow-ssh-rdp|Allows SSH and RDP over TCP ports 22 and 3389|
    |fw-allow-health-checks|Allow health checks over TCP port 80|
    |fw-allow-lb-access|Allow traffic in the 10.10.0.0/16 subnet|
    
5. (Optional) View the contents of each firewall rule.
    
6. In the Google Cloud console, in the **Navigation menu** (![Navigation menu](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation menu")), click **View All Products**. In the left hand pane, select **Networking > Network Connectivity > Cloud Routers**.
    

### **View the instance groups**

The instance groups were created for you. Next, you will observe the configuration details.

1. On the **Navigation menu**, click **Compute Engine > VM instances**.  
    Note the two VM instances that start with _instance-group-1_ and _instance-group-2_.
    
2. Click **instance-group-1**.
    
3. Scroll to **Network interfaces**.  
    Note that the instance group is in _subnet-a_, and its internal IP address is _10.10.20.2_.
    
4. Return to the **VM instances** page, and repeat steps 2 and 3 for **instance-group-2**.  
    Note that this instance group is in _subnet-b_, and its internal IP address is _10.10.30.2_.
    

### **Create a VM for testing**

You create a VM called _utility-vm_ in _subnet-a_ of the _my-internal-app_ network and use it to test the load balancer.

1. Return to the **VM instances** page, and click **Create instance**.
    
2. Specify the following, and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Name|utility-vm|
    |Region|`us-central1`|
    |Zone|`us-central1-c`|
    |Series|E2|
    |Machine type|e2-medium (2vCPU, 4 GB memory)|
    
3. Click **OS and storage**.
    
    Click **Change** to begin configuring your boot disk and select the following values:
    
    - **Operating system**: `Debian`
    - **Version**: `Debian GNU/Linux 12 (bookworm) x86/64, amd64`
4. Click **Networking**.
    
5. For **Network interfaces**, click **default**.
    
6. Set the network interface properties and values as shown in the following table, and leave the remaining properties as their default values:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Network|my-internal-app|
    |Subnetwork|subnet-a|
    |Primary internal IPv4 address|Ephemeral (Custom)|
    |Custom ephemeral IP address|10.10.20.50|
    |External IPv4 address|None|
    
7. Click **Done**.
    
8. Click **Create**.  
    Wait for the new VM to be created.
    

### Verify the backends

1. For **utility-vm**, click **SSH** to launch a terminal and connect.  
    If you see the **Allow SSH-in-browser to connect to VMs** pop-up, click **Authorize**.
    
2. To verify the welcome page for **instance-group-1-xxxx**, run the following command:
    

curl 10.10.20.2

Copied!

content_copy

The output is shown below. Note that the server location is set to `us-central1-c`.

<h1>Internal Load Balancing Lab</h1><h2>Client IP</h2>Your IP address : 10.10.20.50<h2>Hostname</h2>Server Hostname:
 instance-group-1-1zn8<h2>Server Location</h2>Region and Zone: us-central1-c

3. To verify the welcome page for **instance-group-2-xxxx**, run the following command:

curl 10.10.30.2

Copied!

content_copy

The output is shown below. Note that the server location is set to `us-central1-a`.

<h1>Internal Load Balancing Lab</h1><h2>Client IP</h2>Your IP address : 10.10.20.50<h2>Hostname</h2>Server Hostname:
 instance-group-2-q5wp<h2>Server Location</h2>Region and Zone: us-central1-a

Which of these fields identifies the location of the backend?

Server Hostname

Client IP

Server Location

Submit

**Note:** This will be useful when verifying that the load balancer sends traffic to both backends.

4. Close the SSH terminal to **utility-vm**:

exit

Copied!

content_copy

Click **Check my progress** to verify the objective.

Finish setting up the network infrastructure.

Check my progress

## Task 2. Configure the load balancer

In this task, you configure a regional internal Application Load Balancer to balance traffic between the two backends (_instance-group-1_ in `us-central1-c` and _instance-group-2_ in `us-central1-a`), as shown (the region and zones may vary as per the lab requirement):

![The image shows a VPC network with two subnets, each with a managed instance group. One subnet is used for the blue deployment, and the other is used for the green deploynment. Client traffic to the subnets is handled by the load balancer.](https://cdn.qwiklabs.com/FgrZkcSEqghVxKV14KPVgNzTUMo0lQfmqTgpG45%2BTYA%3D)

### **Start the configuration**

1. In the Google Cloud console, in the **Navigation menu** (![Navigation menu](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation menu")), click **View All Products**. In the left hand pane, select **Networking > Network Services > Load balancing**.
    
2. Click **Create load balancer**.
    
3. Under **Application Load Balancer (HTTP/HTTPS)**, click **next**.
    
4. For **Public facing or internal**, select **internal** and click **next**. This selection creates a regional internal Application Load Balancer. This choice requires the backends to be in a single region `us-central1`.
    
5. For **Cross-region or single region deployment**, select **Best for regional workloads** and click **next**.
    
6. Click **Configure**.
    
7. For **Name**, type **my-ilb**
    
8. For **Region**, select **`us-central1`**
    
9. For **Network**, select **my-internal-app**.
    

The proxy servers that implement the regional internal Application Load Balancer require IP addresses. These IP addresses are allocated automatically from a subnet that you specify.

10. Under **Proxy-only subnet required**, click **Reserve subnet**.
    
11. For **Name**, type **my-proxy-subnet**
    
12. For **IP address range**, type **10.10.40.0/24**
    
13. Click **Add**.  
    Wait for the proxy-only subnet to be created. When that is successful, the console displays the name of the proxy-only subnet followed by the IP address range that you specified.
    

### **Configure the blue-service backend**

This backend service refers to the present ("blue") version of your application.

1. Click **Backend configuration**.
    
2. For **Backend configuration**, for **Create or select backend service**, select **Create a backend service**.
    
3. For **Name**, type **blue-service**.
    
4. In **Backends**, specify the following, and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Instance group|instance-group-1|
    |Port numbers|80|
    
5. Click **Done**.
    
6. For **Health check**, select **Create a health check**.
    
7. Specify the following, and leave the remaining settings as their defaults:
    
    |Property|Value (select option as specified)|
    |---|---|
    |Name|blue-health-check|
    |Protocol|TCP|
    |Port|80|
    |Check interval|10 seconds|
    |Timeout|5 seconds|
    |Healthy threshold|2|
    |Unhealthy threshold|3|
    

**Note:** Health checks determine which instances can receive new connections. This HTTP health check polls instances every ten seconds and waits up to five seconds for a response. After two successful probe attempts, the backend is considered to be healthy. After three failed attempts, the backend is considered to be unhealthy.

8. Click **Save**.
    
9. Click **Create**.
    
10. Verify that there is a blue check mark next to **Backend configuration** in the Google Cloud console. If there isn't, double-check that you have completed all the steps above.
    

### **Configure the green-service backend**

This backend service refers to the new ("green") version of your application.

1. For **Backend configuration**, for **Create or select backend service**, select **Create a backend service**.
    
2. For **Name**, type **green-service**.
    
3. In **Backends**, specify the following, and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Instance group|instance-group-2|
    |Port numbers|80|
    
4. Click **Done**.
    
5. For **Health check**, select **Create a health check**.
    
6. Specify the following, and leave the remaining settings as their defaults:
    
    |Property|Value (select option as specified)|
    |---|---|
    |Name|green-health-check|
    |Protocol|TCP|
    |Port|80|
    |Check interval|10 seconds|
    |Timeout|5 seconds|
    |Healthy threshold|2|
    |Unhealthy threshold|3|
    
7. Click **Save**.
    
8. Click **Create**.
    

Under **Backend services**, you should now see two entries: one for the blue-service and another for the green-service. If you do not see the green-service, you will need to re-do the task _Configure the green-service backend_.

9. Click **Ok**.

### **Configure the "blue-green" routing rule**

Create a routing rule that routes 70% of traffic to the blue-service and 30% of traffic to the green service.

1. Click **Routing rules**.
    
2. In the **Routing rules** panel, for **Mode**, select **Advanded host and path rule**.
    
3. Click **Add host and path rule**.
    
4. For **Hosts**, type *****. The * (asterisk) matches all hosts.
    
5. Traffic management is configured using YAML format. Examine the following YAML code, and then copy and paste it into line 1 of the multi-line field **Path matcher (matches, actions, and services)**.
    

defaultService: regions/us-central1/backendServices/blue-service
name: matcher1
routeRules:
 - matchRules:
     - prefixMatch: /
   priority: 0
   routeAction:
     weightedBackendServices:
       - backendService: regions/us-central1/backendServices/blue-service
         weight: 70
       - backendService: regions/us-central1/backendServices/green-service
         weight: 30

Copied!

content_copy

6. Click **Done**.

### **Configure the default routing rule**

When traffic does not match any of the other routing rules, the load balancer uses the default routing rule. Even though the rule you configured is designed to match all traffic, the default routing rule is required. You will configure the default routing rule to use the blue-service backend.

1. Click **(Default) Route traffic to backend "" for any unmatched hosts**.
    
2. In the **Edit host and path rule** panel, for **Service**, select **blue-service**, and then click **Done**.
    

### **Configure the frontend**

The frontend forwards traffic to the backends.

1. Click **Frontend configuration**.
    
2. Specify the following, and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Subnetwork|subnet-b|
    |IP address|Ephemeral (Custom)|
    |Custom ephemeral IP address|10.10.30.5|
    
3. Click **Done**.
    

### **Review and create the load balancer**

1. (Optional) Click **Review and finalize**. Review the **Backend** and **Frontend**.
    
2. Click **Create**.  
    Wait for the load balancer to be created before starting the next task.
    

Click **Check my progress** to verify the objective.

Configure the load balancer.

Check my progress

## Task 3. Test the load balancer

In this task, you verify that the _my-ilb_ IP address forwards most of the traffic to the _blue-service_ running on _instance-group-1_ in _`us-central1-c`_.

### **Access the load balancer**

1. In the **Navigation menu**, click **Compute Engine > VM instances**.
    
2. For **utility-vm**, click **SSH** to launch a terminal and connect.
    
3. To verify that the load balancer forwards traffic, run the following command:
    

curl 10.10.30.5

Copied!

content_copy

The output should look like this:

<h1>Internal Load Balancing Lab</h1><h2>Client IP</h2>Your IP address : 10.10.20.50<h2>Hostname</h2>Server Hostname:
 instance-group-2-1zn8<h2>Server Location</h2>Region and Zone: YOUR_LAB_ZONE

As expected, traffic is forwarded from the load balancer (10.10.30.5) to either the blue-service backend or the green-service backend.

4. Run the same command a few times:

curl 10.10.30.5
curl 10.10.30.5
curl 10.10.30.5
curl 10.10.30.5
curl 10.10.30.5
curl 10.10.30.5
curl 10.10.30.5
curl 10.10.30.5
curl 10.10.30.5
curl 10.10.30.5

Copied!

content_copy

Most responses should come from _instance-group-1_ in `us-central1-c`, which is the blue-service. Fewer responses come from _instance-group-2_ in `us-central1-a`, which is the green-service. (Recall that you configured the load balancer to route 70% of the traffic to the blue-service.) If you do not see that most responses come from _instance-group-1_, run the commands again.

## Task 4. Review

In this lab, you created two managed instance groups in the `us-central1` region. You also created some firewall rules. The firewall rules allow traffic from clients and the health checkers to the managed instance groups. You configured a regional internal Application Load Balancer, using the managed instance groups as backends. Finally, you tested the load balancer to ensure that it works as expected.