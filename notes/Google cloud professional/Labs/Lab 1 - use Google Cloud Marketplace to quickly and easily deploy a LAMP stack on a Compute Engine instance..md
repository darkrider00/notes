
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

## Task 2. Use Cloud Marketplace to deploy a LAMP stack

1. In the Google Cloud Console, on the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **Marketplace**.
    
2. In the search bar, type `LAMP` and then press **ENTER**.
    
3. In the search results, click **Bitnami package for LAMP**.
    
    If you choose another LAMP stack, such as the Google Click to Deploy offering, the lab instructions will not work as expected.
    
4. On the LAMP page, click **GET STARTED**.
    
5. On the Agreements page, check the box for **Terms and agreements**, and click **AGREE**.
    
6. On the **Successfully agreed to terms** pop up, click **DEPLOY**.
    
    If prompted, click on Enable for the Compute Engine API and the Infrastructure Manager API.
    
7. For **Zone**, select the deployment zone to `ZONE` .
    
8. For **Machine Type**, select **E2** as the **Series** and **e2-medium** as the **Machine Type**.
    
9. Leave the remaining settings as their defaults.
    
10. Click **Deploy**.
    
11. If a **Welcome to Deployment Manager** message appears, click **Close** to dismiss it.
    

**Note:** Warnings may appear as the deployment is happening. You can disregard these for this lab.

The status of the deployment appears in the console window: **lampstack-1 is being deployed**. When the deployment of the infrastructure is complete, the status changes to **lampstack-1 has been deployed**.

After the software is installed, a summary of the details for the instance, including the site address, is displayed.

Click _Check my progress_ to verify the objective.

Use Cloud Marketplace to deploy a LAMP stack

Check my progress

## Task 3. Verify your deployment

1. When the deployment is complete, click the **Site address** link in the right pane. (If the website is not responding, wait 30 seconds and try again.) If you see a redirection notice, click on that link to view your new site.
    
    Alternatively, you can click **Visit the site** in the **Get started with Bitnami package for LAMP** section of the page. A new browser tab displays a congratulations message. This page confirms that, as part of the LAMP stack, the Apache HTTP Server is running.
    

**Note:** If you can't see the web page in the browser on your corporate laptop: If possible, exit any corporate VPN/network and try again. Enter the IP address on another device, such as a tablet or even a phone.

## Congratulations!

In this lab, you deployed a LAMP stack to a Compute Engine instance.

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



A LAMP (Linux, Apache, MySQL, Perl/PHP/Python) is one of the most common software stacks for the web's most popular applications. Its generic software stack model has largely interchangeable component

- click on start lab 
- sign in with credentials 

![[Pasted image 20250314170631.png]]

- clcik on market place
- ![[Pasted image 20250314171314.png]]

![[Pasted image 20250314171438.png]]

![[Pasted image 20250314171519.png]]

![[Pasted image 20250314171547.png]]

click on enable 

changed the settings as epr doc and deplyed 

![[Pasted image 20250314171715.png]]

- ![[Pasted image 20250314171838.png]]

- **:** Warnings may appear as the deployment is happening. You can disregard these for this lab.

![[Pasted image 20250314172913.png]]

lamp stack has been deployed 

to verify to to the site page in right pane 
![[Pasted image 20250314173014.png]]

More information about bitnami LAMP stack :

https://docs.bitnami.com/google/

