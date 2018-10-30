
[Source](https://aws.amazon.com/getting-started/tutorials/update-an-app/?trk=gs_card "Permalink to How to Update an Elastic Beanstalk App – AWS")

# How to Update an Elastic Beanstalk App – AWS

#  Update an Application with AWS Elastic Beanstalk  

This tutorial will cover how to update your existing application and then how to delete your Elastic Beanstalk environment, which includes your application. This tutorial is a continuation from the [Launch an Application with AWS Elastic Beanstalk][45] tutorial, so please go through that tutorial first if you haven't already. This tutorial will cover how to update your existing application and then how to get rid of your Elastic Beanstalk environment, which includes your application.  

#### Updating an Application with AWS Requires an Account

[Create a Free Account in Minutes][46]

* * *

Receive twelve months of access to the [AWS Free Usage Tier][47] and enjoy AWS Basic Support features including, 24x7x365 customer service, support forums, and more.  

 

##  Step 1: Update Your Application Code

* * *

a. Navigate to the directory where you downloaded the [php_v1.zip][48] file in the previous tutorial.

_Windows Users_: To unzip the php-v1.zip file, **right click **on the _php-v1.zip _file, click **Extract All**..., then click **Extract**.  

_Mac Users_: **Double click **on the _php-v1.zip_ file, and this will automatically unzip the file into a _php-v1_ folder in the same directory.  

* * *

b. Navigate into the newly unzipped _php-v1_ directory. Open index.php using your favorite text editor. You will make a small edit here that is an example of an application change. Look on line 26 for _
Congratulations!
_. Replace _Congratulations!_, with** Application Updated! **in between the 
 and 
 tags. Then **save** the _index.php_ file (overwriting the original).  

[

![Getting-Started-EB2-1c][49]

][50]

(click to zoom)  

![Getting-Started-EB2-1c][49]

* * *

Next you will need to zip your application so it can be uploaded to AWS as an update package.  

_Windows users_: Please select **Windows** below to see how to create the zipped application file.

_Mac & Linux users_: Please select **Mac/Linux** below to see how to create the zipped application file.  
* Windows
* Mac/Linux
* #### Windows __

c. Select all 6 items (including the _.ebextensions_ directory), **right-click** on _.ebextensions_, select **Send to**, and then click on **Compressed (zipped) folder**.  

[

![Getting-Started-EB2-1e - windows][51]

][52]

(click to zoom)  

![Getting-Started-EB2-1e - windows][51]
* * *

d. Rename the newly created zip file to **php-v2.zip**.  

_Note_: On some Windows systems the _.zip_ part of the file name may be hidden (see the example image).  

[

![Getting-Started-EB2-1e2 - windows][53]

][54]

(click to zoom)  

![Getting-Started-EB2-1e2 - windows][53]
* #### Mac/Linux __

c. _OSX users_: Open a terminal window by pressing **command + space** and typing **terminal** in the search window. Then press **enter** to open the terminal window.

_Linux users_: Open a terminal window.  

[

![Getting-Started-CLI-OSX1][55]

][56]

(click to zoom)  

![Getting-Started-CLI-OSX1][55]

* * *

d. Next, you need to **navigate to the directory where you downloaded the php-v1.zip file** (the default location for file downloads is the _Downloads_ directory so the example here uses that directory; if you downloaded to a different directory, change to that directory instead). (ex. _cd ~/Downloads/php-v2_)

When you are in the directory with the _index.php _file you modified in step 1 part b, zip the files (and a hidden directory called .ebextensions) by typing** zip –r php-v2.zip .e* *** to create _php-v2.zip_ with the updated PHP project in it.  

[

![Getting-Started-EB2-1e2 - mac][57]

][58]

(click to zoom)  

![Getting-Started-EB2-1e2 - mac][57]

##  Step 2: Upload Your Updated Application to Elastic Beanstalk 

* * *

a. Click [here][59] to open the Elastic Beanstalk console. Within the Elastic Beanstalk dashboard, click on **php-sample-app** at the top of your screen, and this should show a drop-down menu where you should select** Application Versions**.  

[

![Getting-Started-EB2-2a][60]

][61]

(click to zoom)

![Getting-Started-EB2-2a][60]

* * *

b. Here you should see one entry in the _Version Label_ column titled _First Release_. The _Source_ column for this entry should show the _php-v1.zip_ file we uploaded in the [previous tutorial][45]. Click on **Upload**, enter **Second Release** for _Version_ label, then **Sample PHP App Update** for _Description_. Click **Browse**, then navigate to the location where your _php-v2.zip_ file is located, Select the php-v2.zip file and click **Upload**.  
  

[

![Getting-Started-EB2-2b][62]

][63]

(click to zoom)  

![Getting-Started-EB2-2b][62]

* * *

c. You should now see _Second Release_ within the application versions table. **Check the box** for _Second Release_, then click **Deploy**. You should see your _Environment_ defaulted to _phpSampleApp-env_. Leave the default settings here and click **Deploy**. Lastly, click **Elastic Beanstalk** in the top left hand corner of the web page.  

[

![Getting-Started-EB2-2c][64]

][65]

(click to zoom)  

![Getting-Started-EB2-2c][64]

* * *

d. **Click on the green box **titled _phpSampleApp-env_ to see the view of your application's environment.  

[

![Getting-Started-EB2-green_box][66]

][67]

(click to zoom)  

![Getting-Started-EB2-green_box][66]

* * *

e. Here, you can see a _Recent Events_ section that displays your application being updated.  

[

![Getting-Started-EB2-2d][68]

][69]

(click to zoom)  

![Getting-Started-EB2-2d][68]

##  Step 3: Accessing Your Updated Elastic Beanstalk Application

* * *

a. Once you see _Environment update completed successfully_ within _Recent Events_, **click on your application URL** toward the center top of the screen to view your updated application.  

[

![Getting-Started-EB2-3a][70]

][71]

(click to zoom)

![Getting-Started-EB2-3a][70]

* * *

b. You will see that instead of the _Congratulations!_ text that existed in version 1 of your application the text has been updated to version 2 with the heading _Application Updated!_

Congratulations! You have successfully updated your AWS Elastic Beanstalk application.  

[

![Getting-Started-EB2-3b][72]

][73]

(click to zoom)

![Getting-Started-EB2-3b][72]

##  Step 4: Terminate Your Environment

* * *

a. To delete your application (and stop using the AWS resources associated with your application), access your Elastic Beanstalk application dashboard, click on **Actions** in the top right-hand corner, then select **Terminate Environment**.  

[

![Getting-Started-EB2-4a][74]

][75]

(click to zoom)

![Getting-Started-EB2-4a][74]

* * *

b. You will be presented with a warning/confirmation screen. Click **Terminate** to continue.

_Note_: It may take a couple of minutes for the environment to completely shut down.  

[

![Getting-Started-EB2-4b][76]

][77]

(click to zoom)  

![Getting-Started-EB2-4b][76]

##  Next Steps

* * *

Now that you have an Elastic Beanstalk application up and running, the next tutorial will walk you through registering a domain name so your website/application can be easy to access.

[Getting a Domain for Your Application »][78]  

[45]: https://aws.amazon.com/getting-started/tutorials/launch-an-app/
[46]: https://portal.aws.amazon.com/gp/aws/developer/registration/index.html
[47]: https://aws.amazon.com/free/
[48]: http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/samples/php-v1.zip
[49]: https://d1.awsstatic.com/Getting%20Started/update-an-app/Getting-Started-EB2-1c.5682cb1d7655464986d2076ae7f5fdd0857c8d6e.png "Getting-Started-EB2-1c"
[50]: https://aws.amazon.com#aws-element-modal-02717b4d-0165-4cf6-9132-82d56414da6b
[51]: https://d1.awsstatic.com/Getting%20Started/update-an-app/Getting-Started-EB2-1e%20-%20windows.4c286afb4f2b7c5e4ea02aaf36192675a414c268.png "Getting-Started-EB2-1e - windows"
[52]: https://aws.amazon.com#aws-element-modal-265f6877-a94a-460c-8320-1f3c330b8c0a
[53]: https://d1.awsstatic.com/Getting%20Started/update-an-app/Getting-Started-EB2-1e2%20-%20windows.0f744c0526c12f297431d9083fc271aeb48043dc.png "Getting-Started-EB2-1e2 - windows"
[54]: https://aws.amazon.com#aws-element-modal-39f19f6e-12d7-4485-a60f-8012dad45187
[55]: https://d1.awsstatic.com/Getting%20Started/s3/s3-from-the-cli/Getting-Started-CLI-OSX1.abf1fee024ab3d2efa21fae43d7b2ead1596bd39.png "Getting-Started-CLI-OSX1"
[56]: https://aws.amazon.com#aws-element-modal-4547596f-e05c-419d-bb00-fb8673787e0b
[57]: https://d1.awsstatic.com/Getting%20Started/update-an-app/Getting-Started-EB2-1e2%20-%20mac.4eb1586e9aa5e46390a92c3c24142938ee8df0c7.png "Getting-Started-EB2-1e2 - mac"
[58]: https://aws.amazon.com#aws-element-modal-54213ba8-9319-46aa-994d-820ac4c656c8
[59]: https://console.aws.amazon.com/elasticbeanstalk/home?region=us-east-1#/applications?applicationNameFilter=
[60]: https://d1.awsstatic.com/Getting%20Started/update-an-app/Getting-Started-EB2-2a.c5181eec4f73e1f88f9daa2463823a7fb92038c0.png "Getting-Started-EB2-2a"
[61]: https://aws.amazon.com#aws-element-modal-27126fb8-ed29-45a9-9cf9-87fbc4b5f7bf
[62]: https://d1.awsstatic.com/Getting%20Started/update-an-app/Getting-Started-EB2-2b.b78e3a9b5773e9b850311e69a85e7ac6ff3e87f4.png "Getting-Started-EB2-2b"
[63]: https://aws.amazon.com#aws-element-modal-52ecae20-00dd-44a5-b8fe-8bbdfa7e4ca8
[64]: https://d1.awsstatic.com/Getting%20Started/update-an-app/Getting-Started-EB2-2c.568c40e9a9e4db73534d319f6c32f66c322c8987.png "Getting-Started-EB2-2c"
[65]: https://aws.amazon.com#aws-element-modal-e9269a35-0c48-4133-9e71-2268089b080c
[66]: https://d1.awsstatic.com/Getting%20Started/update-an-app/Getting-Started-EB2-green_box.f7b981fbc3ac7574f925ca30b2f6cc9022ae6c53.png "Getting-Started-EB2-green_box"
[67]: https://aws.amazon.com#aws-element-modal-0f24d1d3-4208-4c3c-9bdd-dec60536dc60
[68]: https://d1.awsstatic.com/Getting%20Started/update-an-app/Getting-Started-EB2-2d.0560b65af7bc4860f6ac3c22d44edef39760da8a.png "Getting-Started-EB2-2d"
[69]: https://aws.amazon.com#aws-element-modal-23bfab98-59c6-4208-815c-e36b6a771bcf
[70]: https://d1.awsstatic.com/Getting%20Started/update-an-app/Getting-Started-EB2-3a.6493dc08c78fa95acee51738935730d3a97b3721.png "Getting-Started-EB2-3a"
[71]: https://aws.amazon.com#aws-element-modal-e367bc27-c53a-489c-b811-7960f0020d50
[72]: https://d1.awsstatic.com/Getting%20Started/update-an-app/Getting-Started-EB2-3b.25f955f831367b2f303c56cae616de8c760b942a.png "Getting-Started-EB2-3b"
[73]: https://aws.amazon.com#aws-element-modal-d1b607dc-92a2-4e2d-9cf8-640398b162ff
[74]: https://d1.awsstatic.com/Getting%20Started/update-an-app/Getting-Started-EB2-4a.6b22f807c8280d8cb1abb45718b30101156802c4.png "Getting-Started-EB2-4a"
[75]: https://aws.amazon.com#aws-element-modal-3c3c3540-b93d-465b-94b4-4b2c784268b3
[76]: https://d1.awsstatic.com/Getting%20Started/update-an-app/Getting-Started-EB2-4b.cf7febb6b622b0c884931e58157678c422147a6d.png "Getting-Started-EB2-4b"
[77]: https://aws.amazon.com#aws-element-modal-08e7600f-a1a0-44bf-aadc-0dd1f74a0f9b
[78]: https://aws.amazon.com/getting-started/tutorials/get-a-domain/
