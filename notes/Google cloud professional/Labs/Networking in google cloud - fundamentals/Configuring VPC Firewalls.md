
## Overview

In this lab, you investigate [Virtual Private Cloud (VPC)](https://cloud.google.com/vpc) networks and create firewall rules to allow and deny access to a network and instances.

You begin by creating an automatic VPC network, a custom VPC network, and some VPC instances in those networks. You verify that the default-allow-ssh firewall rule is working and then compare this to the user created custom network to verify no ingress is allowed without custom firewall rules.

After deleting the default network, you use firewall rule priorities,to allow both ingress and egress of network traffic to your VMs.

### Objectives

In this lab, you will learn how to:

- Create an auto-mode network, a custom-mode network, and associated subnetworks.
- Investigate firewall rules in the default network and then delete the default network.
- Use features of firewall rules for more precise and flexible control of connections.

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
    
    "Username"
    
    Copied!
    
    content_copy
    
    You can also find the **Username** in the **Lab Details** panel.
    
4. Click **Next**.
    
5. Copy the **Password** below and paste it into the **Welcome** dialog.
    
    "Password"
    
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

### Activate Google Cloud Shell

Google Cloud Shell is a virtual machine that is loaded with development tools. It offers a persistent 5GB home directory and runs on the Google Cloud.

Google Cloud Shell provides command-line access to your Google Cloud resources.

1. In Cloud console, on the top right toolbar, click the Open Cloud Shell button.
    
    ![Highlighted Cloud Shell icon](https://cdn.qwiklabs.com/WGBFVIap4CrFWut%2BGdNFzNxeelWYHF1IqYSMFH6Ouq4%3D)
    
2. Click **Continue**.
    

It takes a few moments to provision and connect to the environment. When you are connected, you are already authenticated, and the project is set to your _PROJECT_ID_. For example:

![Project ID highlighted in the Cloud Shell Terminal](https://cdn.qwiklabs.com/hmMK0W41Txk%2B20bQyuDP9g60vCdBajIS%2B52iI2f4bYk%3D)

**gcloud** is the command-line tool for Google Cloud. It comes pre-installed on Cloud Shell and supports tab-completion.

- You can list the active account name with this command:

gcloud auth list

Copied!

content_copy

**Output:**

Credentialed accounts:
 - <myaccount>@<mydomain>.com (active)
</mydomain></myaccount>

**Example output:**

Credentialed accounts:
 - google1623327_student@qwiklabs.net

- You can list the project ID with this command:

gcloud config list project

Copied!

content_copy

**Output:**

[core]
project = <project_id>
</project_id>

**Example output:**

[core]
project = qwiklabs-gcp-44776a13dea667a6

**Note:** Full documentation of **gcloud** is available in the [gcloud CLI overview guide](https://cloud.google.com/sdk/gcloud) .

## Task 1. Create VPC networks and instances

In this task, you create an automatic VPC network and custom VPC network, and some initial VPC instances in those networks.

1. On the Google Cloud console title bar, click **Activate Cloud Shell** (![Activate Cloud Shell icon](https://cdn.qwiklabs.com/ep8HmqYGdD%2FkUncAAYpV47OYoHwC8%2Bg0WK%2F8sidHquE%3D)) to open Cloud Shell. If prompted, click **Continue**.
2. To create the network _mynetwork_ with auto subnets, run the following command:

gcloud compute networks create mynetwork --subnet-mode=auto

Copied!

content_copy

**Note:** When an auto mode VPC network is created, one subnet from each region is automatically created within it. These automatically created subnets use a set of predefined IP ranges that fit within the 10.128.0.0/9 CIDR block.

You will now create a network with custom subnets. You can choose any private RFC 1918 CIDR block for the primary IP address range of the subnets.

3. To create the network _privatenet_ with custom subnets, run the following command:

gcloud compute networks create privatenet \
--subnet-mode=custom

Copied!

content_copy

4. To create a custom subnet in the privatenet network, run the following command:

gcloud compute networks subnets create privatesubnet \
--network=privatenet --region=Region \
--range=10.0.0.0/24 --enable-private-ip-google-access

Copied!

content_copy

5. To create some instances to use later for testing in all networks, run these commands:

gcloud compute instances create default-vm-1 \
--machine-type e2-micro \
--zone=Zone 1 --network=default

Copied!

content_copy

gcloud compute instances create mynet-vm-1 \
--machine-type e2-micro \
--zone=Zone 1 --network=mynetwork

Copied!

content_copy

gcloud compute instances create mynet-vm-2 \
--machine-type e2-micro \
--zone=Zone 2 --network=mynetwork

Copied!

content_copy

gcloud compute instances create privatenet-bastion \
--machine-type e2-micro \
--zone=Zone  --subnet=privatesubnet --can-ip-forward

Copied!

content_copy

gcloud compute instances create privatenet-vm-1 \
--machine-type e2-micro \
--zone=Zone  --subnet=privatesubnet

Copied!

content_copy

Click _Check my progress_ to verify the objective.

Create VPC networks and instances

Check my progress

## Task 2. Investigate the default network

In this task, you explore the default network and verify that the default-allow-ssh firewall rule is working. Later, you delete the default-vm-1 instance and default network because you no longer need it.

Return to the Cloud console and view the firewall rules.

1. On the **Navigation menu**, click **VPC network > Firewall**.

The following four default rules are created for the default network:

![Four default firewall ingress rules](https://cdn.qwiklabs.com/%2B3rX%2BBQoV4F%2Fs0b%2BSi9SndCb%2BjMo60W8vKASrh9dXL4%3D)

Remember, all networks also have the following 2 rules, which are not displayed in the console:

![Default deny all ingress and default deny all egress rules](https://cdn.qwiklabs.com/tv2tBmwKQMI9SNKmTAn%2F8%2FiUtUpvDfm260URbfnCC6o%3D)

To check that the default-allow-ssh firewall rule is working, ssh into the default-vm-1 instance in the default network and test it.

2. On the **Navigation menu**, click **Compute Engine > VM instances** to display a list of VM instances.
    
3. In the row for the **default-vm-1** instance, click **SSH**.
    

You should connect successfully via SSH to the instance because of the default-allow-ssh rule. You can ping `www.google.com` to test the egress connectivity. Press **Ctrl+C** to stop the ping.

### Delete the default-vm-1 instance

Now delete the default-vm-1 instance because you no longer need it.

1. In the **Navigation menu**, click **Compute Engine > VM instances**, select the **default-vm-1** instance and then click **Delete**.
    
2. In the confirmation box, click **Delete**.
    

### Delete the default network

**Note:** Because the default network allows relatively open access, we recommend that you delete it for production projects.

1. On the **Navigation menu**, click **VPC network > VPC networks** to display the list of VPC networks in the Cloud console.
    
2. Click the **default** network to view the network details.
    
3. Click **Delete VPC Network**.
    
4. In the confirmation box, click **Delete**.
    
5. Wait for the network to be deleted and verify that the default network is no longer displayed on the VPC Networks page.
    

## Task 3. Investigate the user-created networks

In this task, you explore the user-created networks to verify no ingress is allowed without custom firewall rules.

### Verify that no ingress is allowed without custom firewall rules

Remember, all networks have the following 2 rules (which will not be displayed in the Console) to block all incoming traffic and allow all outgoing traffic. Unlike the default network, user-created networks do not have any other rules by default, so currently no inbound traffic is allowed.

![Default deny all ingress and default deny all egress rules](https://cdn.qwiklabs.com/tv2tBmwKQMI9SNKmTAn%2F8%2FiUtUpvDfm260URbfnCC6o%3D)

1. On the **Navigation menu**, click **Compute Engine > VM instances** to display a list of VM instances.
    
2. In the row for **mynet-vm-1** or **mynet-vm-2**, click **SSH**.
    

You should **NOT** be able to connect via SSH to the instances.

You will now try to SSH into an instance from the Cloud Shell.

3. Switch back to or reopen Cloud Shell.
    
4. To try to ssh into the **mynet-vm-2** instance, run the following command:
    

gcloud compute ssh qwiklabs@mynet-vm-2 --zone Zone 2

Copied!

content_copy

If prompted, type `Y` and press **Enter** twice to proceed.

We should **NOT** be able to connect via SSH to the instances. There is currently no inbound access allowed. Igonre the error message **ERROR: (gcloud.compute.ssh) [/usr/bin/ssh] exited with return code [255]**

## Task 4. Create custom ingress firewall rules

In this task, you use Cloud Shell as your client host to test SSH connectivity to the instances. The external IP address of the Cloud Shell instance can be easily retrieved.

However, the IP address of your Cloud Shell instance can change if you close and reopen it, or if it is recycled due to inactivity. This should not be a problem during this lab. For a "real" project, you would allow the IP address of your SSH client host and there should not be a problem.

**Note:** As you just verified, the browser-based console SSH feature used to connect to VM instances does not currently work. If you want to allow that, you need a firewall rule that allows the source IP address. However, source IP addresses for browser-based SSH sessions are dynamically allocated by the Cloud console and can vary from session to session.

For the feature to work, you must allow connections either from any IP address, or from Google's IP address range, which you can retrieve using public SPF records. Either of these options may pose unacceptable risks, depending on your requirements. Instead, you would allow the IP address of the SSH clients you are using to connect.

### Allow SSH access from Cloud Shell

1. Switch back to or reopen Cloud Shell.
    
2. To retrieve the external IP address of the Cloud Shell instance, run the following commands:
    

ip=$(curl -s https://api.ipify.org)
echo "My External IP address is: $ip"

Copied!

content_copy

**Sample output** (your IP will be different):

My External IP address is: 35.229.72.135

3. To add a firewall rule that allows port 22 (SSH) traffic from the Cloud Shell IP address, run the following command:

gcloud compute firewall-rules create \
mynetwork-ingress-allow-ssh-from-cs \
--network mynetwork --action ALLOW --direction INGRESS \
--rules tcp:22 --source-ranges $ip --target-tags=lab-ssh

Copied!

content_copy

This firewall rule is also given a target tag of _lab-ssh_, which means it applies only to instances that are tagged with the lab-ssh tag.

4. To view the firewall rule in the Cloud console, on the **Navigation menu**, click **VPC network > Firewall**.

It will look similar to the following, but your IP address will be different:

![Configuration for ingress lab-ssh firewall](https://cdn.qwiklabs.com/9uKhUJ%2FQAhtDY%2B5b5FXwBXuOImH%2F38MeUcSK7O6MzEk%3D)

This firewall rule will be applied only to instances tagged with _lab-ssh_. It is currently not being applied to any instances.

**Note:** You have just created and applied a firewall rule using a tag. One issue with tags is that they must be added to instances and could possibly be added or removed inadvertently. Firewall rules can also be applied to instances by the service account used. These rules will be applied automatically to all instances that use the specified service account.

5. To add the lab-ssh network tag to the **mynet-vm-2** and **mynet-vm-1** instances, run the following commands in Cloud Shell:

gcloud compute instances add-tags mynet-vm-2 \
    --zone Zone 2 \
    --tags lab-ssh
gcloud compute instances add-tags mynet-vm-1 \
    --zone Zone 1 \
    --tags lab-ssh

Copied!

content_copy

### Stateful firewalls

In VPC networks, firewall rules are stateful. So for each initiated connection tracked by allow rules in one direction, the return traffic is automatically allowed, regardless of any rules.

1. To ssh into the **mynet-vm-2** instance, run the following command in Cloud Shell:

gcloud compute ssh qwiklabs@mynet-vm-2 --zone Zone 2

Copied!

content_copy

It will take several seconds to negotiate the SSH keys, but the connection should succeed. This verifies that the firewall rule is allowing the traffic.

2. Type `exit` to log off the **mynet-vm-2** instance.
    
3. To ssh into the **mynet-vm-1** instance, run the following command in Cloud Shell:
    

 gcloud compute ssh qwiklabs@mynet-vm-1 --zone Zone 1

Copied!

content_copy

This connection should also succeed because the **mynet-vm-1** instance is in the same network, and the firewall rule you created is allowing access to all instances.

### Allow all instances on the same network to communicate via ping

1. While still logged in to the **mynet-vm-1** instance, try pinging the **mynet-vm-2** instance with the command shown below. (Replace the _[PROJECT_ID]_ with the PROJECT_ID for your lab exercise.)

 ping mynet-vm-2.Zone 2.c.[PROJECT_ID].internal

Copied!

content_copy

The ping command will not succeed. Even though the **mynet-vm-1** and the **mynet-vm-2** instances are in the same VPC network, all traffic is blocked by default unless there is a firewall rule allowing it.

2. Press **Ctrl+C** to stop ping if needed. Do not log out of the **mynet-vm-1** instance yet.
    
3. To open a new Cloud Shell window, click **Open a new tab** (**+**).
    
4. To add a firewall rule that allows ALL instances in the mynetwork VPC to ping each other, run the following command:
    

gcloud compute firewall-rules create \
mynetwork-ingress-allow-icmp-internal --network \
mynetwork --action ALLOW --direction INGRESS --rules icmp \
--source-ranges 10.128.0.0/9

Copied!

content_copy

**Note:** This firewall rule does not use a target-tag and therefore applies to all instances in the network by default. There is no need to tag any instances for this firewall to take effect. This kind of firewall rule is useful if all instances in a network need the same rule, but should also be used with caution because they affect all instances.

5. Switch back to the first Cloud Shell session that is connected to **mynet-vm-1** and run the ping again. This time it should work.

 ping mynet-vm-2.Zone 2.c.[PROJECT_ID].internal

Copied!

content_copy

Notice that the hostname _mynet-vm-2_ resolved to the internal IP address of the instance. The internal IP will start with _10.132.0_ (for example, _10.132.0.2_). Google Cloud resolves internal hostnames for you.

6. Press **Ctrl+C** to stop ping.
    
7. You can also try pinging the internal IP address directly and that will also work. Press **Ctrl+C** to stop ping.
    
8. To locate the external IP address of **mynet-vm-2**, on the **Navigation menu**, click **Compute Engine > VM instances**.
    
9. Click on **mynet-vm-2**, locate and copy the external IP address of the instance.
    
10. From the Cloud Shell session that is connected to **mynet-vm-1**, try to ping the external IP address of the **mynet-vm-2** instance:
    

 ping <external_ip_of_mynet-vm-2>
</external_ip_of_mynet-vm-2>

Copied!

content_copy

This should **NOT** work. When you ping the external IP address, the connection goes through the internet gateway, which causes the request to be NATed. The request is now coming from the _external_ IP address of the mynet-vm-1 instance. The firewall rule is to only allow ICMP requests that come from _internal_ IP addresses.

11. Press **Ctrl+C** to stop ping.

Click _Check my progress_ to verify the objective.

Create custom ingress firewall rules

Check my progress

## Task 5. Set the firewall rule priority

In this task, you set the firewall rule priority to deny ICMP traffic. You then verify that any traffic that does not match the rule priority is denied.

So far, all the rules created have been ingress allow rules, so the priority has not been important. Firewall rules can be both allow and deny, can specify ingress and egress, and have a priority from 0 to 65,535. If you do not set a priority, the default is 1,000. Rules are evaluated based on priority, starting from the lowest value. The first rule that matches gets applied.

1. In the first Cloud Shell session, verify that you are still connected to the **mynet-vm-1** instance. You can tell because the prompt will be: `qwiklabs@mynet-vm-1:~$`.

If not connected, use the following command to reconnect:

 gcloud compute ssh qwiklabs@mynet-vm-1 --zone Zone 1

Copied!

content_copy

2. Verify that you can still ping the **mynet-vm-2** instance:

 ping mynet-vm-2.Zone 2.c.[PROJECT_ID].internal

Copied!

content_copy

3. Press **Ctrl+C** to stop ping.
    
4. Switch to your second Cloud Shell window (or open a new one).
    
5. In the second Cloud Shell, create a firewall ingress rule to deny ICMP traffic from any IP with a priority of 500:
    

gcloud compute firewall-rules create \
mynetwork-ingress-deny-icmp-all --network \
mynetwork --action DENY --direction INGRESS --rules icmp \
--priority 500

Copied!

content_copy

6. Switch back to the first Cloud Shell connected to the **mynet-vm-1** instance, and try to ping the **mynet-vm-2** instance:

 ping mynet-vm-2.Zone 2.c.[PROJECT_ID].internal

Copied!

content_copy

It should no longer work. This new rule has a priority of 500, where the allow rule is 1,000.

7. Press **Ctrl+C** to stop ping.

Now change the deny rule to a priority of 2,000.

8. In the second Cloud Shell, modify the firewall rule just created and change the priority to `2000`:

gcloud compute firewall-rules update \
mynetwork-ingress-deny-icmp-all \
--priority 2000

Copied!

content_copy

9. Switch back to the first Cloud Shell connected to the **mynet-vm-1** instance, and try to ping the **mynet-vm-2** instance again:

 ping mynet-vm-2.Zone 2.c.[PROJECT_ID].internal

Copied!

content_copy

This time it will work because the deny rule has a lower priority, so the allow rule is the first matching rule.

10. Press **Ctrl+C** to stop ping.

## Task 6. Configure egress firewall rules

In this task, you create an egress firewall rule and set the priority to 10,000. You then verify that both ingress and egress rule allow that traffic.

1. From the second Cloud Shell window, list all the current firewall rules:

gcloud compute firewall-rules list \
--filter="network:mynetwork"

Copied!

content_copy

Currently, the VMs are still able to ping each other because the rule that denies ICMP has a higher priority than the allow ICMP rule.

Now try an egress rule.

2. Create a firewall egress rule to block ICMP traffic from any IP with a priority of `10000`:

gcloud compute firewall-rules create \
mynetwork-egress-deny-icmp-all --network \
mynetwork --action DENY --direction EGRESS --rules icmp \
--priority 10000

Copied!

content_copy

3. List all the current firewall rules again:

gcloud compute firewall-rules list \
--filter="network:mynetwork"

Copied!

content_copy

Notice that the egress rule priority is set to 10,000, which is much higher than the rules created earlier.

4. Switch back to the first Cloud Shell connected to the **mynet-vm-1** instance and try to ping the **mynet-vm-2** instance:

 ping mynet-vm-2.Zone 2.c.[PROJECT_ID].internal

Copied!

content_copy

**It should no longer work**. Even though the egress rule has a much higher priority of 10,000, it is still blocking traffic. This is because for traffic to be allowed, there must be both an ingress and egress rule allowing that traffic. The priority of ingress rules does not affect the priority of egress rules.

5. Press **Ctrl+C** to stop ping.

Click _Check my progress_ to verify the objective.

Create a firewall rule with priority and egress firewall rule.

Check my progress

## Congratulations!

In this lab, you did the following:

- Created an auto-mode network, a custom-mode network, and associated subnetworks.
- Investigated firewall rules in the default network, and then deleted the default network.
- Used firewall rule features for more precise and flexible control of connections.