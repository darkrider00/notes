(https://partner.cloudskillsboost.google/focuses/495660348/reviews?parent=course_session)

infoThis lab may incorporate AI tools to support your learning.

Lab instructions and tasks

expand_less

- [Overview](https://partner.cloudskillsboost.google/paths/79/course_templates/35/labs/520472#step1)
- [Setup and requirements](https://partner.cloudskillsboost.google/paths/79/course_templates/35/labs/520472#step2)
- [Task 1. Configure a custom network with VPC flow logs](https://partner.cloudskillsboost.google/paths/79/course_templates/35/labs/520472#step3)
- [Task 2. Create an Apache web server](https://partner.cloudskillsboost.google/paths/79/course_templates/35/labs/520472#step4)
- [Task 3. Verify that network traffic is logged](https://partner.cloudskillsboost.google/paths/79/course_templates/35/labs/520472#step5)
- [Task 4. Export the network traffic to BigQuery to further analyze the logs](https://partner.cloudskillsboost.google/paths/79/course_templates/35/labs/520472#step6)
- [Task 5. Add VPC flow log aggregation](https://partner.cloudskillsboost.google/paths/79/course_templates/35/labs/520472#step7)
- [Congratulations!](https://partner.cloudskillsboost.google/paths/79/course_templates/35/labs/520472#step8)
- [End your lab](https://partner.cloudskillsboost.google/paths/79/course_templates/35/labs/520472#step9)

## Overview

In this lab, you will configure a network to record traffic to and from an Apache web server using VPC Flow Logs. You will then export the logs to BigQuery to analyze them.

### Objectives

In this lab, you will learn how to perform the following tasks:

- Configure a custom network with VPC flow logs.
- Create an Apache web server.
- Verify that network traffic is logged.
- Export the network traffic to BigQuery to further analyze the logs.
- Setup VPC flow log aggregation.

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
    
    student-04-ee301021a234@qwiklabs.net
    
    Copied!
    
    content_copy
    
    You can also find the **Username** in the **Lab Details** panel.
    
4. Click **Next**.
    
5. Copy the **Password** below and paste it into the **Welcome** dialog.
    
    ZF6CWiJ7kHfE
    
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

## Task 1. Configure a custom network with VPC flow logs

### Create the custom network

By default, VPC Flow Logs are disabled for a network. Therefore, you will create a new custom-mode network and enable VPC flow logs.

1. In the Google Cloud console, in the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), select **VPC network > VPC networks**.
    
2. Click **Create VPC Network**.
    
3. Specify the following and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Name|vpc-net|
    |Description|Enter an optional description|
    
4. For **Subnet creation mode**, click **Custom**.
    
5. Specify the following and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Name|vpc-subnet|
    |Region|`us-west1`|
    |IP address range|10.1.3.0/24|
    |Flow Logs|On|
    

**Note:** Turning on VPC flow logs doesn't affect performance, but some systems generate a large number of logs, which can increase costs. If you click on **Configure logs** you'll notice that you can modify the aggregation interval and sample rate. This allows you to trade off longer interval updates for lower data volume generation which lowers logging costs. For more information on this, refer to the [log sampling and processing](https://cloud.google.com/vpc/docs/using-flow-logs#log-sampling) documentation.

6. Click **Done**.
7. Click **Create**.

Wait for the network to be created before continuing.

### Create the firewall rule

In order to serve HTTP and SSH traffic on the network, you need to create a firewall rule.

1. In the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), select **VPC network > Firewall**.
    
2. Click **CREATE FIREWALL RULE**.
    
3. Specify the following and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Name|allow-http-ssh|
    |Network|vpc-net|
    |Targets|Specified target tags|
    |Target tags|http-server|
    |Source filter|IPv4 Ranges|
    |Source IPv4 ranges|0.0.0.0/0|
    |Protocols and ports|Specified protocols and ports, and then _check_ tcp, _type:_ 80, 22|
    

**Note:** Make sure to include the **/0** in the **Source IPv4 ranges** to specify all networks.

4. Click **Create**.

Click _Check my progress_ to verify the objective.

Assessment Completed!

Configure a custom network with VPC Flow Logs

Check my progress

Assessment Completed!

## Task 2. Create an Apache web server

### Create the web server

1. In the **Navigation menu**, select **Compute Engine > VM instances**.
    
2. Click **Create instance**.
    
3. Specify the following and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Name|web-server|
    |Region|`us-west1`|
    |Zone|`us-west1-a`|
    |Series|E2|
    |Machine type|e2-micro|
    
4. Click **Networking**.
    
5. For **Network tags**, type `http-server`.
    
6. For **Network interfaces**, click **default**.
    
7. Specify the following and leave the remaining settings as their defaults:
    
    |Property|Value (type value or select option as specified)|
    |---|---|
    |Network|vpc-net|
    |Subnetwork|vpc-subnet (10.1.3.0/24)|
    
8. Click **Done**.
    
9. Click **Create**.
    

### Install Apache

Configure the VM instance that you created as an Apache web server and overwrite the default web page.

1. For **web-server**, click **SSH** to launch a terminal and connect.
    
2. In the **web-server** SSH terminal, update the package index:
    
    sudo apt-get update
    
    Copied!
    
    content_copy
    
3. Install the apache2 package:
    
    sudo apt-get install apache2 -y
    
    Copied!
    
    content_copy
    
4. To create a new default web page by overwriting the default, run the following:
    
    echo '<!doctype html><html><body><h1>Hello World!</h1></body></html>' | sudo tee /var/www/html/index.html
    
    Copied!
    
    content_copy
    
5. Exit the SSH terminal:
    
    exit
    
    Copied!
    
    content_copy
    

Click _Check my progress_ to verify the objective.

Create an Apache web server

Check my progress

## Task 3. Verify that network traffic is logged

### Generate network traffic

1. Return to the **VM instances** page in the Cloud console.
2. For **web-server**, click on the **External IP** to access the server.

**Note:** You should see the **Hello World!** welcome page that you configured. Alternatively, you can access the server in a new tab by navigating to http://_Enter the external IP Address_.

### Find your IP address

Find the IP address of the computer you are using. One easy way to do this is to go to a website that provides this address.

1. Open a browser in a new tab.
2. Go to [Google.com](https://www.google.com/) and search for `what's my IP`. It will either directly reply with your IP or give you a list of sites that perform this service.
3. Ensure that the IP address only contains numerals (IPv4) and is not represented in hexadecimal (IPv6).
4. Copy your IP address. It will be referred to as _YOUR_IP_ADDRESS_.

### Access the VPC flow logs

1. On the Google Cloud console title bar, in the Search field, type **Logging**, click Search, and then click **Logging**.
2. In the **Log fields** panel, under **RESOURCE TYPE**, click **Subnetwork**. In the Query results pane, entries from the subnetwork logs appear.
3. In the **Log fields** panel, under **LOG NAME**, click **compute.googleapis.com/vpc_flows**. In the Query results panel, entries from the VPC flow logs appear. If you do not see **compute.googleapis.com/vpc_flows**, wait a few minutes for this log type to show up.
4. Enable the **Show query** button.
5. In the Query builder box, at the end of line 2, press **Enter** to create a new line.
6. On line 3, enter _YOUR_IP_ADDRESS_ and click **Run Query**.

**Note:** If you do not see the **vpc_flows** filter option or any logs after running the query, you might have to wait a few minutes and refresh. If the **vpc_flows** filter option or logs still do not appear, click on the **External IP** of the **web-server** a few times to generate more traffic. Then, check the **vpc_flows** filter option again and rerun the query.

7. Expand one of the log entries.
8. Within the entry, expand the **jsonPayload** and then expand the **connection**.

Which fields does the connection contain?

Source IP address

Source port

Destination IP address

Destination port

The IANA protocol number

Submit

You can explore other fields within the log entry before continuing to the next task.

## Task 4. Export the network traffic to BigQuery to further analyze the logs

### Create an export sink

1. On the Google Cloud console title bar, type **Logs explorer** in the **Search** field, then select **Logs explorer** from **Search Results**.
2. Under the **RESOURCE TYPE**, click **Subnetwork**. In the Query results pane, entries for all available subnetworks appear.
3. Under the **LOG NAME** filter, click **compute.googleapis.com/vpc_flows**. In the Query results pane, only the VPC flow log entries are shown.
4. Select **Actions > Create Sink**.
5. For the **Sink name**, type `bq_vpcflows`, and click **NEXT**.
6. In the **Select sink service** drop-down list, select **BigQuery dataset**.
7. In the **Select BigQuery dataset** drop-down list, select **Create new BigQuery dataset**.
8. For **Dataset ID**, enter `bq_vpcflows`, and click **CREATE DATASET**.
9. Click **NEXT** twice.
10. Click **CREATE SINK**.

### Generate log traffic for BigQuery

Now that the network traffic logs are being exported to BigQuery, you need to generate more traffic by accessing the web-server several times. Using Cloud Shell, you can `curl` the IP address of the web-server several times.

1. In the **Navigation menu**, select **Compute Engine > VM instances**.
2. Note the **External IP** address for the **web-server** instance. It will be referred to as _EXTERNAL_IP_.
3. Click **Activate Cloud Shell** (![Activate Cloud Shell icon](https://cdn.qwiklabs.com/ep8HmqYGdD%2FkUncAAYpV47OYoHwC8%2Bg0WK%2F8sidHquE%3D)).
4. If prompted, click **Continue**.
5. Store the _EXTERNAL_IP_ in an environment variable in Cloud Shell:

export MY_SERVER=<Enter the EXTERNAL_IP here>

Copied!

content_copy

6. Access the web-server 50 times from Cloud Shell:

for ((i=1;i<=50;i++)); do curl $MY_SERVER; done

Copied!

content_copy

### Visualize the VPC flow logs in BigQuery

1. In the Cloud console, in the **Navigation menu**, click **BigQuery**.
2. If prompted, click **Done**.
3. In the left pane, expand the **bq_vpcflows** dataset to reveal the table. You might have to first expand the **Project ID** to reveal the dataset.
4. Click on the name of the table. It should start with **compute_googleapis**.
5. Click on the **Details** tab.
6. Copy the _Table ID_ value under Table info.

**Note:** If you do not see the **bq_vpcflows** dataset or if it does not expand, wait and refresh the page.

7. Click the + icon to open a new BidQuery Editor tab.
    
8. Add the following to the BigQuery **Editor** and replace **your_table_id** with _TABLE_ID_ while retaining the accents (`) on both sides:
    

#standardSQL
SELECT
jsonPayload.src_vpc.vpc_name,
SUM(CAST(jsonPayload.bytes_sent AS INT64)) AS bytes,
jsonPayload.src_vpc.subnetwork_name,
jsonPayload.connection.src_ip,
jsonPayload.connection.src_port,
jsonPayload.connection.dest_ip,
jsonPayload.connection.dest_port,
jsonPayload.connection.protocol
FROM
`your_table_id`
GROUP BY
jsonPayload.src_vpc.vpc_name,
jsonPayload.src_vpc.subnetwork_name,
jsonPayload.connection.src_ip,
jsonPayload.connection.src_port,
jsonPayload.connection.dest_ip,
jsonPayload.connection.dest_port,
jsonPayload.connection.protocol
ORDER BY
bytes DESC
LIMIT
15

Copied!

content_copy

9. Click **Run**.

**Note:** If you get an error, ensure that you did not remove the **#standardSQL** part of the query. If it still fails, ensure that the TABLE_ID did not include the Project ID.

Which columns does the results table contain?

Destination IP address and port

Protocol

Sum of bytes sent

Source IP address and port

Subnet name

VPC name

Submit

### Analyze the VPC flow logs in BigQuery

The previous query gave you the same information that you saw in the Cloud console. Now, you will change the query to identify the top IP addresses that have exchanged traffic with your **web-server**.

1. Create a new query in the BigQuery **Editor** with the following and replace **your_table_id** with _TABLE_ID_ while retaining the accents (`) on both sides:

#standardSQL
SELECT
jsonPayload.connection.src_ip,
jsonPayload.connection.dest_ip,
SUM(CAST(jsonPayload.bytes_sent AS INT64)) AS bytes,
jsonPayload.connection.dest_port,
jsonPayload.connection.protocol
FROM
`your_table_id`
WHERE jsonPayload.reporter = 'DEST'
GROUP BY
jsonPayload.connection.src_ip,
jsonPayload.connection.dest_ip,
jsonPayload.connection.dest_port,
jsonPayload.connection.protocol
ORDER BY
bytes DESC
LIMIT
15

Copied!

content_copy

2. Click **Run**.

**Note:** The results table now has a row for each source IP and is sorted by the highest amount of bytes sent to the **web-server**. The top result should reflect your Cloud Shell IP address.

**Note:** Unless you accessed the **web-server** after creating the export sink, you will not see your machine's IP address in the table.

You can generate more traffic to the **web-server** from multiple sources and query the table again to determine the bytes sent to the server.

Click _Check my progress_ to verify the objective.

Export the network traffic to BigQuery to further analyze the logs

Check my progress

## Task 5. Add VPC flow log aggregation

In this task, you will now explore a new release of [VPC flow log volume reduction](https://cloud.google.com/vpc/docs/using-flow-logs#log-sampling). Not every packet is captured into its own log record. However, even with sampling, log record captures can be quite large.

You can balance your traffic visibility and storage cost needs by adjusting specific aspects of logs collection, which you will explore in this section.

### Setting up aggregation

1. In the Console, navigate to the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)) and select **VPC network > VPC networks**.
    
2. Click **vpc-net**.
    
3. In the **Subnets** tab, click **vpc-subnet**:
    

![VPC subnets in Subnets tab](https://cdn.qwiklabs.com/loPbGvCESaB2oiby%2FYRCmr8qwwOlSoEo2G4bQwjPeSk%3D)

4. Click **Edit > Advanced Settings** to expose the following fields:

![Flow log settings additional fields](https://cdn.qwiklabs.com/zeVvGMnBf81G7wcXHmYe%2BEwNbT3%2BOiZwuiEAT6a7ezs%3D)

The purpose of each field is explained below.

- **Aggregation time interval:** Sampled packets for a time interval are aggregated into a single log entry. This time interval can be 5 sec (default), 30 sec, 1 min, 5 min, 10 min, or 15 min.
    
- **Metadata annotations:** By default, flow log entries are annotated with metadata information, such as the names of the source and destination VMs or the geographic region of external sources and destinations. This metadata annotation can be turned off to save storage space.
    
- **Log entry sampling:** Before being written to the database, the number of logs can be sampled to reduce their number. By default, the log entry volume is scaled by 0.50 (50%), which means that half of entries are kept. You can set this from 1.0 (100%, all log entries are kept) to 0.0 (0%, no logs are kept).
    

5. Set the **Aggregation Interval** to **30 seconds**.
    
6. Set the **Secondary sampling rate** to **25%**.
    
7. Click **Save**. You should see the following message:
    

![Estimated logs generated per day notification](https://cdn.qwiklabs.com/X1bEDNMrLRomcnHD0AAzR7Bne%2FiMjDDjwyptAVQY6hY%3D)

Setting the aggregation level to 30 seconds can reduce your flow logs size by up to _83%_ compared to the default aggregation interval of 5 seconds. Configuring your flow log aggregation can seriously affect your traffic visibility and storage costs.

## Congratulations!

You have configured a VPC network, enabled VPC Flow Logs, and created a web server in that network. Then, you generated HTTP traffic to the web server, viewed the traffic logs in the Cloud console, and analyzed the traffic logs in BigQuery. Finally, you used VPC Flow Log aggregation for balancing your traffic visibility and storage cost.

There are multiple use cases for VPC Flow Logs. For example, you might use VPC Flow Logs to determine where your applications are being accessed from in order to optimize network traffic expense, to create HTTP load balancers to balance traffic globally, or to deny unwanted IP addresses with Cloud Armor.