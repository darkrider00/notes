
## Objectives

In this lab, you learn how to perform the following tasks:

- Create a Cloud Storage bucket and place an image into it.
- Create a Cloud SQL instance and configure it.
- Connect to the Cloud SQL instance from a web server.
- Use the image in the Cloud Storage bucket on a web page.

## Task 1. Sign in to the Google Cloud Console

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
    
    student-01-4fc17a7f36f5@qwiklabs.net
    
    Copied!
    
    content_copy
    
    You can also find the **Username** in the **Lab Details** panel.
    
4. Click **Next**.
    
5. Copy the **Password** below and paste it into the **Welcome** dialog.
    
    zzR710Zp1ykI
    
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

## Task 2. Deploy a web server VM instance

1. In the Google Cloud console, on the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **Compute Engine** > **VM instances**.
    
2. Click **Create Instance**.
    
3. For **Name**, type `bloghost`
    
4. For **Region** and **Zone**, select the region and zone assigned by Qwiklabs.
    
5. For **Machine type**, accept the default.
    
6. In the left pane click **OS and storage**, if the **Image** shown is not **Debian GNU/Linux 12 (bookworm)**, click **Change** and select version to **Debian GNU/Linux 12 (bookworm)**.
    
7. Click **Networking**.
    
8. In **Firewall**, click **Allow HTTP traffic**.
    
9. In the left pane, click **Advanced**.
    
10. In **Automation**, copy and paste the following script as the value for **Startup script**:
    

apt-get update
apt-get install apache2 php php-mysql -y
service apache2 restart

Copied!

content_copy

**Note:** Be sure to supply that script as the value of the **Startup script** field. If you accidentally put it into another field, it won't be executed when the VM instance starts.

11. Leave the remaining settings as their defaults, and click **Create**.

**Note:** Instance can take about two minutes to launch and be fully available for use.

12. On the **VM instances** page, copy the **bloghost** VM instance's internal and external IP addresses to a text editor for use later in this lab.

Click _Check my progress_ to verify the objective.

Deploy a web server VM instance

Check my progress

## Task 3. Create a Cloud Storage bucket using the gcloud storage command line

All Cloud Storage bucket names must be globally unique. To ensure that your bucket name is unique, these instructions will guide you to give your bucket the same name as your Google Cloud project ID, which is also globally unique.

Cloud Storage buckets can be associated with either a region or a multi-region location: **US**, **EU**, or **ASIA**. In this activity, you associate your bucket with the multi-region closest to the region and zone that Qwiklabs or your instructor assigned you to.

1. On the **Google Cloud console**, on the top right toolbar, click the **Activate Cloud Shell** ![Activate Cloud Shell icon](https://cdn.qwiklabs.com/ep8HmqYGdD%2FkUncAAYpV47OYoHwC8%2Bg0WK%2F8sidHquE%3D). If a dialog box appears, click **Continue**.
    
2. For convenience, enter your chosen location into an environment variable called LOCATION. Enter one of these commands:
    

export LOCATION=US

Copied!

content_copy

Or

export LOCATION=EU

Copied!

content_copy

Or

export LOCATION=ASIA

Copied!

content_copy

3. In Cloud Shell, the DEVSHELL_PROJECT_ID environment variable contains your project ID. Enter this command to make a bucket named after your project ID:

gcloud storage buckets create -l $LOCATION gs://$DEVSHELL_PROJECT_ID

Copied!

content_copy

If prompted, click **Authorize** to continue.

4. Retrieve a banner image from a publicly accessible Cloud Storage location:

gcloud storage cp gs://cloud-training/gcpfci/my-excellent-blog.png my-excellent-blog.png

Copied!

content_copy

5. Copy the banner image to your newly created Cloud Storage bucket:

gcloud storage cp my-excellent-blog.png gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png

Copied!

content_copy

6. Modify the Access Control List of the object you just created so that it's readable by everyone:

gsutil acl ch -u allUsers:R gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png

Copied!

content_copy

Click _Check my progress_ to verify the objective.

Create a Cloud Storage bucket using the gcloud storage command line

Check my progress

## Task 4. Create the Cloud SQL instance

1. In the Google Cloud console, on the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **SQL**.
    
2. Click **Create instance**.
    
3. For **Choose a database engine**, select **Choose MySQL**.
    
4. For **Choose a Cloud SQL edition**, click **Enterprise** and then select **Sandbox** from the dropdown.
    
5. For **Instance ID,** type **blog-db**, and for **Password** type a password of your choice.
    

**Note:** Choose a password that you remember. There's no need to obscure the password because you use mechanisms to connect that aren't open access to everyone.

6. For **Region**, select the region assigned by Qwiklabs.
    
7. For **Zonal availability**, select **Single zone**.
    
8. Click **Specify Zones**, and then click **Primary Zone**. Select the zone assigned by Qwiklabs.
    

**Note:** This is the same region and zone into which you launched the **bloghost** instance. The best performance is achieved by placing the client and the database close to each other.

9. Click **Create Instance**.

**Note:** Wait for the instance to finish deploying. It will take a few minutes.

10. From the SQL instances details page, under **Connect to this instance**, copy the **Public IP address** for your SQL instance to a text editor for use later in this lab.
    
11. In the left pane, click **Users**, and then click **Add User Account**.
    
12. For **User name**, type `blogdbuser`
    
13. For **Password**, type a password of your choice. Make a note of it.
    
14. Click **Add** to add the user account in the database.
    

**Note:** Wait for the user to be created.

15. In the left pane, click **Connections**, and then click **Networking** tab.
    
16. Click **Add a Network**.
    

**Note:** If you're offered the choice between a **Private IP** connection and a **Public IP** connection, choose **Public IP** for purposes of this lab.

**Note:** The **Add network** button may be unavailable if the user account creation is not yet complete.

17. For **Name**, type `web front end`
    
18. For **Network**, type the external IP address of your **bloghost** VM instance, followed by `/32`
    

The result will look like this:

35.192.208.2/32

**Note:** Be sure to use the external IP address of your VM instance followed by /32. Do not use the VM instance's internal IP address. Do not use the sample IP address shown here.

19. Click **Done** to finish defining the authorized network.
    
20. Click **Save** to save the configuration change.
    

**Note**: If the message appears like **Another operation is in progress**, wait for few minutes until you see the green check for **blog-db** to save the configuration.

Click _Check my progress_ to verify the objective.

Create the Cloud SQL instance

Check my progress

## Task 5. Configure an application in a Compute Engine instance to use Cloud SQL

1. On the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **Compute Engine** > **VM instances**.
    
2. In the VM instances list, click **SSH** in the row for your VM instance **bloghost**.
    
3. In your ssh session on **bloghost**, change your working directory to the document root of the web server:
    

cd /var/www/html

Copied!

content_copy

4. Use the **nano** text editor to edit a file called **index.php**:

sudo nano index.php

Copied!

content_copy

5. Copy and paste the content below into the file:

<html>
<head><title>Welcome to my excellent blog</title></head>
<body>
<h1>Welcome to my excellent blog</h1>
<?php
 $dbserver = "CLOUDSQLIP";
$dbuser = "blogdbuser";
$dbpassword = "DBPASSWORD";
// In a production blog, we would not store the MySQL
// password in the document root. Instead, we would store
//  it in a Secret Manger. For more information see 
// https://cloud.google.com/sql/docs/postgres/use-secret-manager

 try {
  $conn = new PDO("mysql:host=$dbserver;dbname=mysql", $dbuser, $dbpassword);
  // set the PDO error mode to exception
  $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
  echo "Connected successfully";
} catch(PDOException $e) {
  echo "Database connection failed:: " . $e->getMessage();
}

?>
</body></html>

Copied!

content_copy

**Note:** In a later step, you will insert your Cloud SQL instance's IP address and your database password into this file. For now, leave the file unmodified.

6. Press **Ctrl+O**, and then press **Enter** to save your edited file.
    
7. Press **Ctrl+X** to exit the nano text editor.
    
8. Restart the web server:
    

sudo service apache2 restart

Copied!

content_copy

9. Open a new web browser tab and paste into the address bar your **bloghost** VM instance's external IP address followed by **/index.php**. The URL will look like this:

35.192.208.2/index.php

**Note:** Be sure to use the external IP address of your VM instance followed by /index.php. Do not use the VM instance's internal IP address. Do not use the sample IP address shown here. If you see the message that the IP address doesn't support a secure connection, click **Continue to site**.

When you load the page, you will see that its content includes an error message beginning with the words:

Database connection failed: ...

**Note:** This message occurs because you have not yet configured PHP's connection to your Cloud SQL instance.

10. Return to your ssh session on **bloghost**. Use the **nano** text editor to edit **index.php** again. Ensure that you are in the /var/www/html directory.

sudo nano index.php

Copied!

content_copy

11. In the **nano** text editor, replace `CLOUDSQLIP` with the Cloud SQL instance (blog-db) Public IP address that you noted above. Leave the quotation marks around the value in place.
    
12. In the **nano** text editor, replace `DBPASSWORD` with the Cloud SQL database password that you defined above. Leave the quotation marks around the value in place.
    
13. Press **Ctrl+O**, and then press **Enter** to save your edited file.
    
14. Press **Ctrl+X** to exit the nano text editor.
    
15. Restart the web server:
    

sudo service apache2 restart

Copied!

content_copy

16. Return to the web browser tab in which you opened your **bloghost** VM instance's external IP address. When you load the page, the following message appears:

Connected successfully

**Note:** In an actual blog, the database connection status would not be visible to blog visitors. Instead, the database connection would be managed solely by the administrator.

## Task 6. Configure an application in a Compute Engine instance to use a Cloud Storage object

1. In the Google Cloud console, click **Cloud Storage > Buckets**.
    
2. Click the bucket that is named after your Google Cloud project.
    
3. In this bucket, there is an object called **my-excellent-blog.png**. Copy the URL behind the link icon that appears in that object's **Public access** column, or behind the words "Public link" if shown.
    

**Note:** If you see neither a link icon nor a "Public link", try refreshing the browser. If you still do not see a link icon, return to Cloud Shell and confirm that your attempt to change the object's Access Control list with the **gsutil acl ch** command was successful.

4. Return to your ssh session on your **bloghost** VM instance.
    
5. Enter this command to set your working directory to the document root of the web server:
    

cd /var/www/html

Copied!

content_copy

6. Use the **nano** text editor to edit **index.php**:

sudo nano index.php

Copied!

content_copy

7. Use the arrow keys to move the cursor to the line that contains the **h1** element. Press **Enter** to open up a new, blank screen line, and then paste the URL you copied earlier into the line.
    
8. Paste this HTML markup immediately before the URL:
    

<img src='

9. Place a closing single quotation mark and a closing angle bracket at the end of the URL:

'>

The resulting line will look like this:

 <img src='https://storage.googleapis.com/qwiklabs-gcp-0005e186fa559a09/my-excellent-blog.png'>

The effect of these steps is to place the line containing `<img src='...'>` immediately before the line containing `<h1>...</h1>`

**Note:** Do not copy the URL shown here. Instead, copy the URL shown by the Storage browser in your own Cloud Platform project.

10. Press **Ctrl+O**, and then press **Enter** to save your edited file.
    
11. Press **Ctrl+X** to exit the nano text editor.
    
12. Restart the web server:
    

sudo service apache2 restart

Copied!

content_copy

13. Return to the web browser tab in which you opened your **bloghost** VM instance's external IP address. When you load the page, its content now includes a banner image.

## Congratulations!

In this lab, you configured a Cloud SQL instance and connected an application in a Compute Engine instance to it. You also worked with a Cloud Storage bucket.

## End your lab

When you have completed your lab, click **End Lab**. Google Cloud Skills Boost removes the resources you’ve used and cleans the account for you.

You will be given an opportunity to rate the lab experience. Select the applicable number of stars, type a comment, and then click **Submit**.

The number of stars indicates the following:

- 1 star = Very dissatisfied
- 2 stars = Dissatisfied
- 3 stars = Neutral
- 4 stars = Satisfied
- 5 stars = Very satisfied

You can close the dialog box if you don't want to provide feedback.

For feedback, suggestions, or corrections, please use the **Support** tab.

Copyright 2022 Google LLC All rights reserved. Google and the Google logo are trademarks of Google LLC. All other company and product names may be trademarks of the respective companies with which they are associated.

## More resources

Read the [Google Cloud Platform documentation on Cloud SQL](https://cloud.google.com/sql/docs/).

Read the [Google Cloud Platform documentation on Cloud Storage](https://cloud.google.com/storage/docs/).

![[Pasted image 20250314190744.png]]

to create a cloud bucket command is 
```
gcloud storage buckets create -l $LOCATION gs://$DEVSHELL_PROJECT_ID
```


internal : 10.138.0.2
external : 34.169.47.174

35.203.145.9 public ip of external instance 

![[Pasted image 20250314192420.png]]

![[Pasted image 20250314193156.png]]

