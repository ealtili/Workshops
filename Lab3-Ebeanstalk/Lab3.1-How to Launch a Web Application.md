
[Source](https://aws.amazon.com/getting-started/tutorials/launch-an-app/?trk=gs_card "Permalink to How to Launch a Web Application – Amazon Web Services")

# How to Launch a Web Application – Amazon Web Services

#  Launch an Applicationwith AWS Elastic Beanstalk  

This step-by-step guide will help you get a sample PHP application up and running with AWS Elastic Beanstalk (EB). EB supports other languages besides PHP, such as Java, .NET, Node.JS, Python, Ruby, Docker, and Go, but the focus of this tutorial will be on PHP (other languages will follow the same process). You will first configure your EB application, then setup your EB environment where your application will be launched into.  

**Did you know? **AWS made it even easier to launch a web application. [Jumpstart your application with Amazon Lightsail >>][45]

#### Launching an Application with AWS Requires an Account

[Create a Free Account in Minutes][46]

* * *

Receive twelve months of access to the [AWS Free Usage Tier][47] and enjoy AWS Basic Support features including, 24x7x365 customer service, support forums, and more.  

 

* * *

In this tutorial, we will be using a pre-built sample PHP application. To download this sample PHP application file, please click [here][48].

When you click [here][49], the AWS management console will open in a new browser window, so you can keep this step-by-step guide open. When this screen loads, enter your **user name** and **password** to get started. Then type in "elastic beanstalk" in the search bar and press **Enter**.  
  

[

![AWS Console Image][50]

][51]

(click to expand)  

![Getting-Started-Launch-an-app-0][52]

##  Step 1: Create a New Application 

* * *

Now that you're in the AWS Elastic Beanstalk dashboard, click on **Create New Application **to create and configure your application.  

[

![Amazon Elastic Beanstalk Start Screen][53]

][54]

(click to expand)  

![Getting-Started-Launch-an-app-1][55]

##  Step 2: Configure your Application

* * *

Fill out the _Application name_ with **php-sample-app** and _Description_ field with **Sample PHP App**. Click **Next** to continue.  

[

![Getting-Started-Launch-an-app-2][56]

][57]

(click to expand)  

![Getting-Started-Launch-an-app-2][56]

##  Step 3: Configure your Environment

* * *

a. For this tutorial, we will be creating a web server environment for our sample PHP application. Click on **Create web server**.  

[

![Getting-Started-Launch-an-app-3a][58]

][59]

(click to enlarge)  

![Getting-Started-Launch-an-app-3a][58]

* * *

b. Click on **Select a platform** next to _Predefined configuration_, then select **PHP**. Next, click on the drop-down menu next to _Environment type_, then select **Single instance**. 

_Note_: an "instance" is referring to Amazon's Elastic Compute Cloud (EC2) compute service. A "single instance" means we will be using one virtual server to deploy our application into. 

We will discuss how to scale and load balance your application in a separate tutorial. Click **Next** to continue.   
  

[

![Getting-Started-Launch-an-app-3b][60]

][61]

(click to enlarge)  

![Getting-Started-Launch-an-app-3b][60]

* * *

c. Under _Source_, select the **Upload your own** option, then click **Choose File** to select the sample **php-v1.zip** file we downloaded earlier. 

Before moving on, double click on the **php-v1.zip** file that you downloaded to your local machine to view the contents within. This will help you better understand what your zip file should look like when working with your own PHP application. PHP does not enforce a strict file structure for applications; flat file structure will work fine.

Click **Next** to continue.  
  

[

![Getting-Started-Launch-an-app-3c][62]

][63]

(click to enlarge)  

![Getting-Started-Launch-an-app-3c][62]

* * *

d. Fill in the values for _Environment name_ with **phpSampleApp-env**. For _Environment URL_, fill in a globally unique value since this will be your public-facing URL; we will use **phpsampleapp-env** in this tutorial, so please choose something different from this one. Lastly, fill _Description_ with **Sample PHP App**. For the _Environment URL_, make sure to click **Check availability** to make sure that the URL is not taken. Click **Next** to continue.   

[

![Getting-Started-Launch-an-app-3d][64]

][65]

(click to enlarge)  

![Getting-Started-Launch-an-app-3d][64]

* * *

e. **Check the box** next to _Create this environment inside a VPC_. Click **Next** to continue.   

[

![Getting-Started-Launch-an-app-3e][66]

][67]

(click to enlarge)  

![Getting-Started-Launch-an-app-3e][66]

* * *

f. On the **Configuration Details** step, you can set configuration options for the instances in your stack. For this tutorial, you don't need to change anything. Click **Next**.  

On the **Environment Tags** step, you can tag all the resources in your stack. For this tutorial, you don't need to tag any resources but can if you would like. Click **Next**.

On the **VPC Configuration** step, select the first AZ listed by checking the box under the **EC2** column. Your list of AZs may look different than the one shown as Regions can have different number of AZs. Click **Next**.  

[

![Getting-Started-Launch-an-app-3g][68]

][69]

(click to enlarge)  

![Getting-Started-Launch-an-app-3g][68]

* * *

g. At the _Permissions_ step, leave everything to their default values, then click **Next** to continue. Then review your _environment configuration_ on the next screen and then click **Launch** to deploy your application. 

_Note_: Launching your application may take a few minutes.  
  

##  Step 4: Accessing your Elastic Beanstalk Application

* * *

a. Go back to the main Elastic Beanstalk dashboard page by clicking on **Elastic Beanstalk**. When your application successfully launched, your application's environment, _phpSampleApp-env_, will show up as a green box. Click on **phpSample-App-env**, which is the green box.  

[

![Getting-Started-Launch-an-app-4a][70]

][71]

(click to enlarge)  

![Getting-Started-Launch-an-app-4a][70]

* * *

b. At the top of the page, you should see a _URL_ field, with a value that contains the _Environment URL_ you specified in step 3 part d. **Click on this URL field**, and you should see a _Congratulations page_.  

[

![Getting-Started-Launch-an-app-4b][72]

][73]

(click to enlarge)  

![Getting-Started-Launch-an-app-4b][72]

* * *

Congratulations! You have successfully launched a sample PHP application using AWS Elastic Beanstalk.  

[

![Getting-Started-Launch-an-app-congratulations][74]

][75]

(click to enlarge)  

![Getting-Started-Launch-an-app-congratulations][74]

##  Next Steps

* * *

Now that you have an Elastic Beanstalk application up and running, the next tutorial will walk you through updating your application.  

[Update Your Elastic Beanstalk Application »][76]  


[45]: https://lightsail.aws.amazon.com/ls/webapp/home/resources
[46]: https://portal.aws.amazon.com/gp/aws/developer/registration/index.html
[47]: https://aws.amazon.com/free/
[48]: http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/samples/php-v1.zip
[49]: https://console.aws.amazon.com/console/home?region=us-west-2
[50]: https://d1.awsstatic.com/Getting%20Started/launch-an-app/Getting-Started-Launch-an-app-0.68f2adc6b67bcec418513577c43b4483c547b5ce.png "AWS Console Image"
[51]: https://aws.amazon.com#aws-element-modal-f7ffa599-4408-40dc-bad0-2a6c2998281b
[52]: https://d1.awsstatic.com/Getting%20Started/launch-an-app/Getting-Started-Launch-an-app-0.68f2adc6b67bcec418513577c43b4483c547b5ce.png "Getting-Started-Launch-an-app-0"
[53]: https://d1.awsstatic.com/Getting%20Started/launch-an-app/Getting-Started-Launch-an-app-1.c6ccaa943177987b6f128117838d9a68f69e47f0.png "Amazon Elastic Beanstalk Start Screen"
[54]: https://aws.amazon.com#aws-element-modal-e0fbc0cf-55df-47d7-aa19-dae17a55dc14
[55]: https://d1.awsstatic.com/Getting%20Started/launch-an-app/Getting-Started-Launch-an-app-1.c6ccaa943177987b6f128117838d9a68f69e47f0.png "Getting-Started-Launch-an-app-1"
[56]: https://d1.awsstatic.com/Getting%20Started/launch-an-app/Getting-Started-Launch-an-app-2.b91fa0fb0b1bfd1ca62ba27468a4494187381ae2.png "Getting-Started-Launch-an-app-2"
[57]: https://aws.amazon.com#aws-element-modal-5caf8da0-b782-47a3-8890-fc9a182ccef8
[58]: https://d1.awsstatic.com/Getting%20Started/launch-an-app/Getting-Started-Launch-an-app-3a.ba7037406a602034c2815e355154ba94df3ba552.png "Getting-Started-Launch-an-app-3a"
[59]: https://aws.amazon.com#aws-element-modal-6b764828-5aa7-4d7c-a0b4-bb4c5576704e
[60]: https://d1.awsstatic.com/Getting%20Started/launch-an-app/Getting-Started-Launch-an-app-3b.3ef2e9cb0beaf9940ab0515eb2cbea758674e3be.png "Getting-Started-Launch-an-app-3b"
[61]: https://aws.amazon.com#aws-element-modal-e28de705-e887-407e-9ed0-ecdd75e6dc9c
[62]: https://d1.awsstatic.com/Getting%20Started/launch-an-app/Getting-Started-Launch-an-app-3c.8e6086a704592f16aaf3faad185098a4c868f96a.png "Getting-Started-Launch-an-app-3c"
[63]: https://aws.amazon.com#aws-element-modal-71e3f7a5-cb17-458a-b533-c682d18e5826
[64]: https://d1.awsstatic.com/Getting%20Started/launch-an-app/Getting-Started-Launch-an-app-3d.7e8c510286ec6535ba6785ad70330f722e8ea04e.png "Getting-Started-Launch-an-app-3d"
[65]: https://aws.amazon.com#aws-element-modal-74ba95ed-9ad0-4f79-ae59-ca31d65cefd9
[66]: https://d1.awsstatic.com/Getting%20Started/launch-an-app/Getting-Started-Launch-an-app-3e.6c27bd7a82038d3e46f55c98006849d3f8cddaf2.png "Getting-Started-Launch-an-app-3e"
[67]: https://aws.amazon.com#aws-element-modal-2022289c-a48a-4a6a-8372-eb507f098706
[68]: https://d1.awsstatic.com/Getting%20Started/launch-an-app/Getting-Started-Launch-an-app-3g.eca1abe8d83c81104fd1d1894e3053d126698b99.png "Getting-Started-Launch-an-app-3g"
[69]: https://aws.amazon.com#aws-element-modal-5d7e35da-2153-42d3-b0ec-2ea8d041073d
[70]: https://d1.awsstatic.com/Getting%20Started/launch-an-app/Getting-Started-Launch-an-app-4a.c40a274f91e93cc7db9b9f35e2e3f58c96d3a7b8.png "Getting-Started-Launch-an-app-4a"
[71]: https://aws.amazon.com#aws-element-modal-19cf1bf3-23f9-40f8-bc5a-7599e81804ad
[72]: https://d1.awsstatic.com/Getting%20Started/launch-an-app/Getting-Started-Launch-an-app-4b.d5f480c12784b1768ecf7fe40e274adb6c942f42.png "Getting-Started-Launch-an-app-4b"
[73]: https://aws.amazon.com#aws-element-modal-c3e23b07-d327-4c1d-8ddf-e0b3d7f5ec46
[74]: https://d1.awsstatic.com/Getting%20Started/launch-an-app/Getting-Started-Launch-an-app-congratulations.15e76e5ccb919f677a02b9c73ebb91315d3fa40e.png "Getting-Started-Launch-an-app-congratulations"
[75]: https://aws.amazon.com#aws-element-modal-b0e890dc-1652-4c5b-8702-db3226ed1f15
[76]: https://aws.amazon.com/getting-started/tutorials/update-an-app/
[77]: https://aws.amazon.com/getting-started/tutorials/launch-an-app/
