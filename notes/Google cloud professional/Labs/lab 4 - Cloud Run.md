
[Cloud Run](https://cloud.google.com/run) is a managed compute platform that enables you to run stateless containers that are invocable via HTTP requests. Cloud Run is serverless: it abstracts away all infrastructure management, so you can focus on what matters most — building great applications.

[Cloud Run](https://cloud.google.com/run) is built from [Knative](https://cloud.google.com/knative/), letting you choose to run your containers either fully managed with Cloud Run, or in your [Google Kubernetes Engine](https://cloud.google.com/kubernetes) cluster with Cloud Run on GKE.

The goal of this lab is for you to build a simple containerized application image and deploy it to Cloud Run.

### Objectives

In this lab, you learn to:

- Enable the Cloud Run API.
- Create a simple Node.js application that can be deployed as a serverless, stateless container.
- Containerize your application and upload to Artifact Registry.
- Deploy a containerized application on Cloud Run.
- Delete unneeded images to avoid incurring extra storage charges.

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

### Reference

### Basic Linux Commands

Below you will find a reference list of a few very basic Linux commands which may be included in the instructions or code blocks for this lab.

|Command -->|Action|.|Command -->|Action|
|---|---|---|---|---|
|**mkdir** (_make directory_)|create a new folder|.|**cd** (_change directory_)|change location to another folder|
|**ls** (_list_ )|list files and folders in the directory|.|**cat** (_concatenate_)|read contents of a file without using an editor|
|**apt-get update**|update package manager library|.|**ping**|signal to test reachability of a host|
|**mv** (_move_ )|moves a file|.|**cp** (_copy_)|makes a file copy|
|**pwd** (_present working directory_ )|returns your current location|.|**sudo** (_super user do_)|gives higher administration privileges|

## Task 1. Enable the Cloud Run API and configure your Shell environment

1. From Cloud Shell, enable the **Cloud Run API** :

gcloud services enable run.googleapis.com

Copied!

content_copy

2. If you are asked to authorize the use of your credentials, do so. You should then see a successful message similar to this one:

Operation "operations/acf.cc11852d-40af-47ad-9d59-477a12847c9e" finished successfully.

**Note:** You can also enable the API using the **APIs & Services** section of the console.

3. Set the compute region:

gcloud config set compute/region us-west1

Copied!

content_copy

4. Create a LOCATION environment variable:

LOCATION="us-west1"

Copied!

content_copy

## Task 2. Write the sample application

In this task, you will build a simple express-based NodeJS application which responds to HTTP requests.

1. In Cloud Shell create a new directory named `helloworld`, then move your view into that directory:

mkdir helloworld && cd helloworld

Copied!

content_copy

2. Next you'll be creating and editing files. To edit files, use `nano` or the Cloud Shell Code Editor by clicking on the **Open Editor** button in Cloud Shell.
    
3. Create a `package.json` file, then add the following content to it:
    

nano package.json

Copied!

content_copy

{
  "name": "helloworld",
  "description": "Simple hello world sample in Node",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "author": "Google LLC",
  "license": "Apache-2.0",
  "dependencies": {
    "express": "^4.17.1"
  }
}

Copied!

content_copy

Most importantly, the file above contains a start script command and a dependency on the Express web application framework.

4. Press **CTRL+X**, then **Y**, then **Enter** to save the `package.json` file.
    
5. Next, in the same directory, create an `index.js` file, and copy the following lines into it:
    

nano index.js

Copied!

content_copy

const express = require('express');
const app = express();
const port = process.env.PORT || 8080;

app.get('/', (req, res) => {
  const name = process.env.NAME || 'World';
  res.send(`Hello ${name}!`);
});

app.listen(port, () => {
  console.log(`helloworld: listening on port ${port}`);
});

Copied!

content_copy

This code creates a basic web server that listens on the port defined by the `PORT` environment variable. Your app is now finished and ready to be containerized and uploaded to Artifact Registry.

6. Press **CTRL+X**, then **Y**, then **Enter** to save the `index.js` file

**Note:** You can use many other languages to get started with Cloud Run. You can find instructions for Go, Python, Java, PHP, Ruby, Shell scripts, and others from the [Quickstarts guide](https://cloud.google.com/run/docs/quickstarts/build-and-deploy).

## Task 3. Containerize your app and upload it to Artifact Registry

1. To containerize the sample app, create a new file named `Dockerfile` in the same directory as the source files, and add the following content:

nano Dockerfile

Copied!

content_copy

# Use the official lightweight Node.js 12 image.
# https://hub.docker.com/_/node
FROM node:12-slim

# Create and change to the app directory.
WORKDIR /usr/src/app

# Copy application dependency manifests to the container image.
# A wildcard is used to ensure copying both package.json AND package-lock.json (when available).
# Copying this first prevents re-running npm install on every code change.
COPY package*.json ./

# Install production dependencies.
# If you add a package-lock.json, speed your build by switching to 'npm ci'.
# RUN npm ci --only=production
RUN npm install --only=production

# Copy local code to the container image.
COPY . ./

# Run the web service on container startup.
CMD [ "npm", "start" ]

Copied!

content_copy

2. Press **CTRL+X**, then **Y**, then **Enter** to save the `Dockerfile` file.
    
3. Now, build your container image using Cloud Build by running the following command from the directory containing the `Dockerfile.` (Note the $GOOGLE_CLOUD_PROJECT environmental variable in the command, which contains your lab's Project ID):
    

gcloud builds submit --tag gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld

Copied!

content_copy

Cloud Build is a service that executes your builds on Google Cloud. It executes a series of build steps, where each build step is run in a Docker container to produce your application container (or other artifacts) and push it to Artifact Registry, all in one command.

Once pushed to the registry, you will see a SUCCESS message containing the image name (`gcr.io/[PROJECT-ID]/helloworld`). The image is stored in Artifact Registry and can be re-used if desired.

4. List all the container images associated with your current project using this command:

gcloud container images list

Copied!

content_copy

5. Register `gcloud` as the credential helper for all Google-supported Docker registries:

gcloud auth configure-docker

Copied!

content_copy

**Note:** You may be prompted **Do you want to continue? (y/N)?** if you are, enter **Y** to agree.

6. To run and test the application locally from Cloud Shell, start it using this standard `docker` command:

docker run -d -p 8080:8080 gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld

Copied!

content_copy

7. In the Cloud Shell window, click on **Web preview** and select **Preview on port 8080**.

This should open a browser window showing the "Hello World!" message. You could also simply use `curl localhost:8080`.

## Task 4. Deploy to Cloud Run

1. Deploying your containerized application to Cloud Run is done using the following command adding your Project-ID:

gcloud run deploy --image gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld --allow-unauthenticated --region=$LOCATION

Copied!

content_copy

The allow-unauthenticated flag in the command above makes your service publicly accessible.

2. When prompted confirm the `service name` by pressing **Enter**.

**Note:** You may be prompted **Do you want enable these APIs to continue (this will take a few minutes)? (y/N)?** if you are, enter **Y** to enable the API needed.

Wait a few moments until the deployment is complete.

On success, the command line displays the service URL:

Service [helloworld] revision [helloworld-00001-xit] has been deployed
and is serving 100 percent of traffic.

Service URL: https://helloworld-h6cp412q3a-uc.a.run.app

You can now visit your deployed container by opening the service URL in any browser window.

**Congratulations!** You have just deployed an application packaged in a container image to Cloud Run. Cloud Run automatically and horizontally scales your container image to handle the received requests, then scales down when demand decreases. In your own environment, you only pay for the CPU, memory, and networking consumed during request handling.

For this lab you used the `gcloud` command-line. Cloud Run is also available via Cloud console.

- From the **Navigation menu**, in the Serverless section, click **Cloud Run** and you should see your `helloworld` service listed:

![Cloud Run tab displaying the helloworld service](https://cdn.qwiklabs.com/VjQNdBvvAlr7BxY91Fqz2%2BrpUyxA5K2uUQDk%2FiwwIag%3D)

## Task 5. Clean up

While Cloud Run does not charge when the service is not in use, you might still be charged for storing the built container image.

1. You can either decide to delete your Google Cloud project to avoid incurring charges, which will stop billing for all the resources used within that project, or simply delete your `helloworld` image using this command :

gcloud container images delete gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld

Copied!

content_copy

2. When prompted to continue type `Y`, and press **Enter**.
    
3. To delete the Cloud Run service, use this command :
    

gcloud run services delete helloworld --region=us-west1

Copied!

content_copy

4. When prompted to continue type `Y`, and press **Enter**.


END YOUR LAB 


![[Pasted image 20250314201626.png]]


![[Pasted image 20250314201639.png]]

![[Pasted image 20250314201714.png]]

![[Pasted image 20250314201927.png]]

![[Pasted image 20250314202025.png]]

above is our unique url containerised application 


For more information on building a stateless HTTP container suitable for Cloud Run from code source and pushing it to Artifact Registry, view:

- [Developing Cloud Run services](https://cloud.google.com/run/docs/developing)
- [Building Containers](https://cloud.google.com/run/docs/building/containers)

Copyright 2022 Google LLC All rights reserved. Google and the Google logo are trademarks of Google LLC. All other company and product names may be trademarks of the respective companies with which they are associated.

[navigate_beforePrevious](https://partner.cloudskillsboost.google/paths/79/course_sessions/22278958/video/521860)

[Nextnavigate_next](https://partner.cloudskillsboost.google/paths/79/course_sessions/22278958/quizzes/521862)

![](https://cdn.qwiklabs.com/assets/labs/start_lab-f45aca49782d4033c3ff688160387ac98c66941d.png)

# Before you begin

1. Labs create a Google Cloud project and resources for a fixed time
2. Labs have a time limit and no pause feature. If you end the lab, you'll have to restart from the beginning.
3. On the top left of your screen, click **Start lab** to begin

Skip

Finish

task_alt

# Score Details

OK

![](https://cdn.qwiklabs.com/assets/lab_enablement_notification/disable_lab-47cff1f6bc3610f58767251ff93c2f99cf4f9040.png)

This content is not currently available

We will notify you via email when it becomes available

[No, thanks](https://partner.cloudskillsboost.google/focuses/489603672/set_up_lab_forward_url?course_template=60&parent=course_session)

Yes, notify me

![](https://cdn.qwiklabs.com/assets/lab_enablement_notification/notifcation_subscribed-2b4f9e51439e1a107488ab58a6e13c3c62ef8855.png)

Great!

We will contact you via email if it becomes available

[Back to screen](https://partner.cloudskillsboost.google/focuses/489603672/set_up_lab_forward_url?course_template=60&parent=course_session)

![](https://cdn.qwiklabs.com/assets/quota_management/quota_empty-2ba3ec879dea3091828ec9cfa060947292e2c554.png)

Got it

![](https://cdn.qwiklabs.com/assets/quota_management/one_lab_quota-77010e9a83e0a6c7543477868b8b808d70222adb.png)

One lab at a time

Confirm to end all existing labs and start this one

Cancel

Confirm

![](https://cdn.qwiklabs.com/assets/labs/open_incognito_window-3ab2004605e88542dd7732361c3fc0e010c7fb6e.png)

[Continue anyway](https://accounts.google.com/AddSession?service=accountsettings&sarp=1&continue=https%3A%2F%2Fconsole.cloud.google.com%2Fhome%2Fdashboard%3Fproject%3Dqwiklabs-gcp-01-bb1a90d0b941#Email=student-04-1ed375fd0fd7@qwiklabs.net)

Cancel

# How satisfied are you with this lab?*

Cancel

Submit

error_outline

# Are you sure? You may not be able to restart the lab, and you'll need to start from the beginning if you do.

Cancel

End Lab

error

# A newer version of this course is available. Your progress will carry over if you choose to upgrade. However, your completion percentage may change if the new version has added or removed any learning activities. Click the preview button to see the course changes before upgrading.

Cancel

[Preview](https://partner.cloudskillsboost.google/paths/79/course_templates/60/preview)


