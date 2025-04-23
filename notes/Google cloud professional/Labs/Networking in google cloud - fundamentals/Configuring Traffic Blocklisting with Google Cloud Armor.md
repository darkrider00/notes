
## Overview

Application Load balancing (HTTP/HTTPS) is implemented at the edge of Google's network in Google's points of presence (POP) around the world. User traffic directed to an Application Load Balancer enters the POP closest to the user and is then load balanced over Google's global network to the closest backend that has sufficient capacity available.

[Google Cloud Armor](https://cloud.google.com/armor) IP blocklists/allowlists enable you to restrict or allow access to your Application Load Balancer at the edge of the Google Cloud, as close as possible to the user and to malicious traffic. This prevents malicious users or traffic from consuming resources or entering your virtual private cloud (VPC) networks.

In this lab, you will verify that an Application Load Balancer with global backends is deployed. This load balancer is automatically provisioned for you during startup. You will then create a VM to test access to the load balancer. Finally, you will stress test the load balancer and blocklist the stress test IP with Google Cloud Armor.

### Objectives

In this lab, you will learn how to perform the following tasks:

- Verify that an Application Load Balancer is deployed.
- Create a VM to test access to the Application Load Balancer.
- Use Google Cloud Armor to blocklist an IP address and restrict access to an Application Load Balancer.

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
    
    student-04-b43da8b82315@qwiklabs.net
    
    Copied!
    
    content_copy
    
    You can also find the **Username** in the **Lab Details** panel.
    
4. Click **Next**.
    
5. Copy the **Password** below and paste it into the **Welcome** dialog.
    
    4Ezo7fedNA09
    
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

## Task 1. Verify the Application Load Balancer is deployed

In this task, you verify that the global Application Load Balancer is deployed. The Application Load Balancer is automatically created when you start the lab. This will be used for a simple web application. This application is deployed to demonstrate the capabilities of Google Cloud Armor.

1. On the Google Cloud console title bar, click **Activate Cloud Shell** (![Activate Cloud Shell icon](https://cdn.qwiklabs.com/ep8HmqYGdD%2FkUncAAYpV47OYoHwC8%2Bg0WK%2F8sidHquE%3D)). If prompted, click **Continue**, and then click **Authorize**.
    
2. Verify that the load balancer is deployed and registered by executing the following command:
    

gcloud compute backend-services get-health web-backend --global

Copied!

content_copy

**Note:** Rerun this command and wait until this command returns that three instances are HEALTHY. You can also monitor it in the console (**Navigation menu > View All Products > Network services > Load balancing**).

3. Retrieve the load balancer IP address by executing the following command:

gcloud compute forwarding-rules describe web-rule --global

Copied!

content_copy

4. Copy the value for the **IPAddress** property.

Keep track of this IP address. It will also be used in a later section.

5. Open a new browser tab and try to visit that IP address `http://{IP_ADDRESS}`.

Replace `{IP_ADDRESS}` with the IP address of the load balancer. Do not include the curly braces when you are asked to provide the IP address.

If you get a message that the IP address doesn't support a secure connection, click **Continue to site**.

Keep refreshing the page until you see a page with a message similar to this:

![Web server notification; the server is in zone X](https://cdn.qwiklabs.com/TejCgv4DW0Lq%2FQg5JjVV6H4dNY%2FEeZPTWo03qa3reCk%3D)

**Note:** It might take a couple of minutes to access the Application Load Balancer. In the meantime, you might get 404 or 502 errors. Keep trying until you see the page of one of the backends.

6. In Cloud shell, use the following `curl` command to access the IP address:

while true; do curl -m1 {IP_ADDRESS}; done

Copied!

content_copy

The responses will be from backends that have been created in different zones.

7. Press **CTRL+C** to stop the previous command.

## Task 2. Create a VM to test access to the load balancer

1. In the Google Cloud console, in the **Navigation menu** (![Navigation Menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation Menu")), click **Compute Engine > VM instances**.
    
2. Click **Create instance**.
    
3. On the **Machine configuration** page, enter the following values:
    
    |**Field**|**Value** (type or select)|
    |---|---|
    |Name|access-test|
    |Region|`us-central1`|
    |Zone|`us-central1-c`|
    
4. Leave everything else at the default and click **Create**.
    
5. Once launched, click the **SSH** button to connect to the instance.
    
6. Run the following command on the instance to access the load balancer:
    

curl -m1 {IP_ADDRESS}

Copied!

content_copy

The output should look similar to:

<!doctype html><html><body><h1>Web server</h1><h2>This server is in zone: projects/104716457480/zones/us-central1-c</h2> </body></html>

Click _Check my progress_ to verify the objective.

Create a VM to test access to the load balancer.

Check my progress

## Task 3. Create a security policy with Google Cloud Armor

### Blocklist the access-test VM

**Note:** You will now create a security policy to blocklist access to the load balancer from the access-test VM. This policy can be used to block access from a malicious client. There are ways to identify the external IP address of a client trying to access your Application Load Balancer. For example, you could examine traffic captured by VPC Flow Logs in BigQuery to determine a high volume of incoming requests.

1. In the Google Cloud console, in the **Navigation menu** (![Navigation Menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation Menu")), click **Compute Engine > VM instances**.
2. Locate and copy the **External IP** address for the **access-test** VM. You will need this in the following steps.
3. In the Google Cloud console, in the **Navigation menu** (![Navigation Menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation Menu")), click **View all products> Networking > Network Security > Cloud Armor policies**.
4. Click **Create policy**.
5. In the **Name** field, type **blocklist-access-test**, and then set the **Default rule action** to **Allow**.
6. Click **Next step**.
7. Click **Add a rule**.
8. Set the following values, leave all other values at their defaults:

|   |   |
|---|---|
|**Property**|**Value**|
|Mode|Basic mode (IP addresses/ranges only)|
|Match|Enter the External IP of the **access-test** VM|
|Action|Deny|
|Response code|404 (Not Found)|
|Priority|1000|

**Note:** Notice that you are setting the Deny status to 404.

8. Click **Save change to rule**.
9. Click **Next step**.
10. Click **+ Add target**.
11. For **Type 1**, select **Backend service (external application load balancer)**.
12. For **Backend Service target 1**, select **web-backend**.
13. Click **Next step**.
14. Click **Done**.
15. Click **Create policy**.

**Note:** Alternatively, you could set the default rule to Deny and only allow list traffic from authorized users/IP addresses.

Wait for the policy to be created before moving to the next step.

### Verify the security policy

1. Return to the SSH session of the access-test VM.
2. Run the `curl` command again on the instance to access the load balancer:

curl -m1 {IP_ADDRESS}

Copied!

content_copy

The output should look as follows.

**Output:**

<!doctype html><meta charset="utf-8"><meta name=viewport content="width=device-width, initial-scale=1"><title>404</title>404 Not Found

**Note:** It might take a couple of minutes for the security policy to take affect. If you are able to access the backends, keep trying until you get the **404** Not Found error.

3. Try accessing the load balancer IP from your local browser. You should still be able to access it as we have only blocklisted the access-test VM.

Click _Check my progress_ to verify the objective.

Create a security policy with Google Cloud Armor.

Check my progress

## Task 4. View Google Cloud Armor logs

1. In the Google Cloud console, in the **Navigation menu** (![Navigation Menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation Menu")), click **View all products> Networking > Network Security > Cloud Armor policies**.
2. Click **blocklist-access-test**.
3. Click **Logs**.
4. Click **View policy logs** and go to the latest logs. If prompted, close the notification.
5. Locate a log with a **404** and expand the log entry.
6. Expand **httpRequest**.
7. The request should be from the **access-test** VM IP address.
8. Explore some of the other log entries.

## Congratulations!

In this lab, you have done the following:

- Verified that the Application Load Balancer was deployed.
- Created a VM to test access to the Application Load Balancer.
- Used Google Cloud Armor to blocklist an IP address and restrict access to an Application Load Balancer.