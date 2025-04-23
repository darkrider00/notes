## Overview

[Google Cloud Armor](https://cloud.google.com/armor) [edge security policies](https://cloud.google.com/armor/docs/security-policy-overview#edge-policies) allow you to restrict access to cached objects on [Cloud CDN](https://cloud.google.com/cdn) (Content Delivery Network) and Cloud Storage. Edge security policies are deployed and enforced at the outermost perimeter of Google's network, upstream of where the Cloud CDN cache resides. Reasons to do this include ensuring that your users do not access objects in storage buckets from restricted geographies, or ensuring that your media distribution is filtering on the geographies that you have a license to do so.

In this lab you create a Google Cloud Storage bucket, upload an image to it, bind it to a load balancer, and then enable Cloud CDN and Cloud Armor edge security policies on it.

### What you'll learn

In this lab, you learn how to:

- Set up a Cloud Storage Bucket with cacheable content
- Create an edge security policy to protect the content
- Validate that the edge security policy is working as expected

## Setup and requirements

### Before you click the Start Lab button

Read these instructions. Labs are timed and you cannot pause them. The timer, which starts when you click **Start Lab**, shows how long Google Cloud resources are made available to you.

This hands-on lab lets you do the lab activities in a real cloud environment, not in a simulation or demo environment. It does so by giving you new, temporary credentials you use to sign in and access Google Cloud for the duration of the lab.

To complete this lab, you need:

- Access to a standard internet browser (Chrome browser recommended).

**Note:** Use an Incognito (recommended) or private browser window to run this lab. This prevents conflicts between your personal account and the student account, which may cause extra charges incurred to your personal account.

- Time to complete the lab—remember, once you start, you cannot pause a lab.

**Note:** Use only the student account for this lab. If you use a different Google Cloud account, you may incur charges to that account.

### How to start your lab and sign in to the Google Cloud console

1. Click the **Start Lab** button. If you need to pay for the lab, a dialog opens for you to select your payment method. On the left is the Lab Details pane with the following:
    
    - The Open Google Cloud console button
    - Time remaining
    - The temporary credentials that you must use for this lab
    - Other information, if needed, to step through this lab
2. Click **Open Google Cloud console** (or right-click and select **Open Link in Incognito Window** if you are running the Chrome browser).
    
    The lab spins up resources, and then opens another tab that shows the Sign in page.
    
    **_Tip:_** Arrange the tabs in separate windows, side-by-side.
    
    **Note:** If you see the **Choose an account** dialog, click **Use Another Account**.
    
3. If necessary, copy the **Username** below and paste it into the **Sign in** dialog.
    
    student-01-6320319953d2@qwiklabs.net
    
    Copied!
    
    content_copy
    
    You can also find the Username in the Lab Details pane.
    
4. Click **Next**.
    
5. Copy the **Password** below and paste it into the **Welcome** dialog.
    
    mP4MWqeTA4Ah
    
    Copied!
    
    content_copy
    
    You can also find the Password in the Lab Details pane.
    
6. Click **Next**.
    
    **Important:** You must use the credentials the lab provides you. Do not use your Google Cloud account credentials.
    
    **Note:** Using your own Google Cloud account for this lab may incur extra charges.
    
7. Click through the subsequent pages:
    
    - Accept the terms and conditions.
    - Do not add recovery options or two-factor authentication (because this is a temporary account).
    - Do not sign up for free trials.

After a few moments, the Google Cloud console opens in this tab.

**Note:** To access Google Cloud products and services, click the **Navigation menu** or type the service or product name in the **Search** field. ![Navigation menu icon and Search field](https://cdn.qwiklabs.com/9Fk8NYFp3quE9mF%2FilWF6%2FlXY9OUBi3UWtb2Ne4uXNU%3D)

### Before you begin

- In Cloud Shell, set your Project ID and create an environment variable for it:

export PROJECT_ID=$(gcloud config get-value project)
echo $PROJECT_ID
gcloud config set project $PROJECT_ID

Copied!

content_copy

## Task 1. Create a Cloud Storage bucket and upload an object

The Cloud Storage bucket will be the origin source for Cloud CDN.

1. In the console, go to **Navigation menu (![Navigation menu](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D))** > **Cloud Storage** > **Buckets**.
    
2. To create a new Cloud Storage bucket, click **CREATE**.
    
3. Set the bucket name as `qwiklabs-gcp-03-614677324c93`
    
4. Click **Continue**.
    
5. For **Location type**, select `Region`, and choose `us-east1`
    
6. Click **Continue**.
    
7. The default storage class for your bucket is `Standard`. Click **Continue**.
    
8. Uncheck `Enforce public access prevention on this bucket` checkbox under **Prevent public access**.
    
9. Choose **Fine-grained** under **Access Control**.
    
10. Click **Continue**.
    
11. Click **Create**.
    

That's it — you've just created a Cloud Storage bucket!

### Upload an Object to the bucket

Now upload an object into the bucket, which you will use later. By default, Cloud Storage buckets are private. As part of this lab, you will make the object available to the Internet.

1. Run the following command in Cloud Shell, to download an image to Cloud Shell. A Google image from the Google homepage is used for this lab.

wget --output-document google.png https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png

Copied!

content_copy

2. Use the `gsutil cp` command to upload the image from the Cloud Shell to the bucket you created:

gsutil cp google.png gs://qwiklabs-gcp-03-614677324c93

Copied!

content_copy

3. Remove the downloaded image from Cloud Shell:

rm google.png

Copied!

content_copy

4. Locate the object you have uploaded to the bucket by navigating to **Cloud Storage > Buckets > `qwiklabs-gcp-03-614677324c93`**.
    
5. Now, click on the three dots on the right side of the object you uploaded and click **Edit access**.
    
6. Click on **Add Entry** and set the entity as **Public** from the drop-down list.
    
7. Click **Save**.
    

![Edit access page, which lists the entities and includes the Save and Cancel buttons](https://cdn.qwiklabs.com/b7J%2FDa%2FQs1ii9RJbtLB9PEBijeY9rdhukZsgf0V76Y0%3D)

Click **Check my progress** to verify the objective.

Create a Cloud Storage Bucket and upload an object

Check my progress

## Task 2. Create a Load Balancer

Cloud CDN and Cloud Armor are components that can be tied to Google's global [Cloud Load Balancing](https://cloud.google.com/load-balancing). In this section, you create an HTTP Load balancer.

1. In the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **View All Products > Network services** > **Load Balancing**.
2. Click **+CREATE LOAD BALANCER**.
3. Under Type of **load balancer**, select **Application Load Balancer (HTTP/HTTPS)** and click **NEXT**.
4. Under **Public facing or internal**, select **Public facing (external)** and click **NEXT**.
5. For **Global or single region deployment**, select **Best for global workloads** and click **NEXT**.
6. For **Load balancer generation**, select **Global external Application Load Balancer** and click **NEXT**.
7. Click **CONFIGURE** button.
8. Name the load balancer as `edge-cache-lb`.

### Create frontend configuration

To create the frontend configuration:

1. Click on **Frontend configuration**.
    
2. For the frontend configuration use HTTP (though HTTPS also works if you have a certificate) and an ephemeral IP address and ensure that you have selected the premium tier network. This is by default.
    
3. Click **Done**.
    

![Frontend configuration page, which includes the load balancer's description](https://cdn.qwiklabs.com/W%2Ftq7MRoTnPDw%2Bvl3uNSZwxbwFEE1txmCee%2FHTIZ8yM%3D)

### Create backend configuration

To create the backend configuration:

1. Click on **Backend configuration**.
    
2. For **Backend services & backend buckets**, click **Create a backend bucket**.
    
3. Set the **Backend bucket name** to `lb-backend-bucket`.
    
4. In the next field, select the Cloud Storage bucket created earlier by clicking the **Browse** button.
    
5. Leave all other values at their defaults.
    
6. Click **Create**.
    

### Create host and path rules

To create host and path rules:

1. Click on **Routing rules** on the left.
    
2. Select **simple host and path rule** under Mode to send any request to the bucket. This is the default option.
    

### Review and create the HTTP Load Balancer

To review and create the HTTP Load Balancer:

1. Click on **Review and finalize**.
2. Review the **Backend services** and **Frontend**.
3. Click on **Create**.

### Get Load Balancer IP

To get the Load Balancer IP from the console:

- Click the load balancer name in the list of load balancers for the project. Note the IPv4 address of the load balancer for the next task. Refer to it as `[LOAD_BALANCER_IP]`.

![The Details page, which includes the highlighted IP:Port address](https://cdn.qwiklabs.com/gEIAdRhQ0Wllm2LutPBRlMAcAgXNbrZH%2FUMny9AgaGI%3D)

### Query the Load Balancer

After a couple minutes, query the load balancer for the object you uploaded. You will need the load balancer IP address and the name of the image.

1. Run the following from CloudShell and replace the LOAD_BALANCER_IP with the IPv4 address of the load balancer:

curl -svo /dev/null http://LOAD_BALANCER_IP/google.png

Copied!

content_copy

**Note:** It might take up to 5 minutes to access the HTTP Load Balancer.

**Output:**

student-cloudshell% curl -svo /dev/null http://34.98.81.123/google.png
*   Trying 34.98.81.123...
* TCP_NODELAY set
* Connected to 34.98.81.123 (34.98.81.123) port 80 (#0)
> GET /google.png HTTP/1.1
> Host: YOUR_IP
> User-Agent: curl/7.64.1
> Accept: */*
>
< HTTP/1.1 200 OK
< X-GUploader-UploadID: ADPycdtoILI76KVsvBvdVGvSfzaxys1m3zYqCepBrmJxAI48ni24cWCRIdNu-53PX3DS6iycxp6xwFbMpwtcHHZQUQmEBxAgng
< Expires: Mon, 13 Dec 2021 22:58:26 GMT
< Date: Mon, 13 Dec 2021 21:58:26 GMT
< Cache-Control: public, max-age=3600
< Last-Modified: Mon, 13 Dec 2021 21:45:57 GMT
< ETag: "8f9327db2597fa57d2f42b4a6c5a9855"
< x-goog-generation: 1639431957957903
< x-goog-metageneration: 2
< x-goog-stored-content-encoding: identity
< x-goog-stored-content-length: 5969
< Content-Type: image/png
< x-goog-hash: crc32c=TeiHTA==
< x-goog-hash: md5=j5Mn2yWX+lfS9CtKbFqYVQ==
< x-goog-storage-class: STANDARD
< Accept-Ranges: bytes
< Content-Length: 5969
< Server: UploadServer

2. Run a few queries with this command:

for i in `seq 1 50`; do curl http://LOAD_BALANCER_IP/google.png; done

Copied!

content_copy

### Confirm content served by Cloud CDN

- Validate that your content is being served from the CDN via CDN or Load Balancing Monitoring by navigating to **Network Services > Cloud CDN**.

![Cloud CDN overview page, with one result populated](https://cdn.qwiklabs.com/7UEDVoyLD6cXCvf7GPS11Wg9EXVz0WD57IqpPKT3ocM%3D)

You should be able to get close to a 100% hit ratio.

Click **Check my progress** to verify the objective.

Create a Load Balancer

Check my progress

## Task 3. Delete the object from Cloud Storage bucket

Now that the cache is populated, delete the object from the bucket. This will reinfore that you are applying the policy to the cache and not the backend.

1. In the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **Cloud Storage > Buckets > `qwiklabs-gcp-03-614677324c93`**.
    
2. Select the object and delete it by clicking the **Delete** button at the top.
    
3. Click **Delete** at the prompt.
    

Click **Check my progress** to verify the objective.

Delete the object from Cloud Storage bucket

Check my progress

## Task 4. Create an edge security policy

Cloud Armor policies are substantiated outside of the HTTP Load Balancer. Once the Cloud Armor policy is deployed, you can then associate it with one or more HTTP Load Balancer Backend Service or Bucket resources, referred to as a Target.

1. In the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **View All Products > Network Security > Cloud Armor policies** and click **Create Policy**.

2. Set the following values, leave all other values at their defaults and click **Next Step**:

|Property|Value (type value or select option as specified)|
|---|---|
|Name|edge-security-policy|
|Policy type|Edge security policy|
|Default rule action|Deny|

3. In **Apply policy to targets** section, click **Add Target** and set the following values:

|Property|Value|
|---|---|
|Type 1|Backend bucket (external application load balancer)|
|Backend Bucket target 1|lb-backend-bucket|

4. Click **Done**.
    
5. Click **Create Policy**.
    

### Validate Edge Security Policy

Now that you've created an edge security policy in front of the back-end bucket, validate that it works as expected.

#### Check the security policy

After a few minutes have passed, you can check that the Cloud Armor policy is running.

From the command line, run the following command, which gives you a 403:

curl -svo /dev/null http://LOAD_BALANCER_IP/google.png

Copied!

content_copy

A 403 error occurs when you do not have permission to accessing a web page or something on a web server.

**Output:**

curl -svo /dev/null http://34.98.81.123/google.png
*   Trying 34.98.81.123...
* TCP_NODELAY set
* Connected to 34.98.81.123 (34.98.81.123) port 80 (#0)
> GET /google.png HTTP/1.1
> Host: YOUR_IP
> User-Agent: curl/7.64.1
> Accept: */*
>
< HTTP/1.1 403 Forbidden
< X-GUploader-UploadID: ADPycdtS6FtJOGIsiWYDrAAE8VFeQuNutcvbGoQe2t8EZxsuspVtmCjyiTv_P3CNktroHMOGFXkTCfG-Jj-rUO60ZGPpEbpqcw
< Content-Type: application/xml; charset=UTF-8
< Content-Length: 111
< Date: Mon, 13 Dec 2021 23:09:35 GMT
< Expires: Mon, 13 Dec 2021 23:09:35 GMT
< Cache-Control: private, max-age=0
< Server: UploadServer

#### Investigate the logs

Next, you check the logs to see the enforced edge security policy.

1. In the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **View All Products > Observability > Logging > Logs Explorer**.
    
2. Enter the below snippet into the query box and click **Run Query**:
    

resource.type:(http_load_balancer) AND jsonPayload.@type="type.googleapis.com/google.cloud.loadbalancing.type.LoadBalancerLogEntry" AND severity>=WARNING

Copied!

content_copy

3. Note the `403 response` and the enforced security policy.

![The Query page, which includes the highlighted 403 response message and its security policy](https://cdn.qwiklabs.com/6oLMK5C%2FszEFTgZb1VOEtFb4z%2BQr%2FFb470LXgCZ5Y8c%3D)

Click **Check my progress** to verify the objective.

Create edge security policy for cloud Armor

Check my progress

### Remove the security policy

To prove that the object is getting delivered from the CDN cache, remove the Cloud Armor security policy and query the object. The origin object has been removed from Cloud Storage, thus illustrating that the object is getting served from the edge cache.

1. In the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click **View All Products > Network Security > Cloud Armor policies > edge-security-policy > Targets**.
2. Select the `lb-backend-bucket` target and click **Remove** to remove the target bucket. Confirm **Remove**.

3. Wait a few minutes, then send another `curl` to the resource in the Cloud Storage bucket:

curl -svo /dev/null http://LOAD_BALANCER_IP/google.png

Copied!

content_copy

You get a `200` response this time. The web page is acting as it is supposed to.

**Output:**

student-cloudshell% curl -svo /dev/null http://34.98.81.123/google.png

 Trying 34.98.81.123...
 TCP_NODELAY set
 Connected to 34.98.81.123 (34.98.81.123) port 80 (#0)
 GET /google.png HTTP/1.1
 Host: YOUR_IP
 User-Agent: curl/7.64.1
 Accept: */*

  HTTP/1.1 200 OK
  X-GUploader-UploadID: ADPycdtI7f49P3MSuZSZ8vl6RwfwmnIDJ59EeSKp7UPvLPawdaiRHXiNWLtseQTxUxceWOvSLvpYmT3pWVkV4qeIP7M
  Date: Mon, 13 Dec 2021 23:06:46 GMT
  Last-Modified: Mon, 13 Dec 2021 21:45:57 GMT
  ETag: "8f9327db2597fa57d2f42b4a6c5a9855"
  x-goog-generation: 1639431957957903
  x-goog-metageneration: 2
  x-goog-stored-content-encoding: identity
  x-goog-stored-content-length: 5969
  Content-Type: image/png
  x-goog-hash: crc32c=TeiHTA==
  x-goog-hash: md5=j5Mn2yWX+lfS9CtKbFqYVQ==
  x-goog-storage-class: STANDARD
  Accept-Ranges: bytes
  Content-Length: 5969
  Server: UploadServer
  Age: 1621
  Cache-Control: public,max-age=3600
 { [775 bytes data]
 Connection #0 to host 34.98.81.123 left intact
 Closing connection 0

Try it a couple of times and see if you get a 403 status code.