
[Source](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/nodejs-dynamodb-tutorial.html?refid=gs_card "Permalink to Deploying a Node.js Application with DynamoDB to Elastic Beanstalk")

# Deploying a Node.js Application with DynamoDB to Elastic Beanstalk

This tutorial and [sample application][1] walks you through the process of deploying a Node.js application that uses the AWS SDK for JavaScript in Node.js to interact with Amazon DynamoDB. You'll create a DynamoDB table that is external to the AWS Elastic Beanstalk environment, and configure the application to use this external table instead of creating one in the environment. In a production environment, you keep the table independent of the Elastic Beanstalk environment to protect against accidental data loss and enable you to perform [blue/green deployments][2]. 

The tutorial's sample application uses a DynamoDB table to store user-provided text data. The sample application uses [configuration files][3] to create the table and an Amazon Simple Notification Service topic. It also shows how to use a [package.json file][4] to install packages during deployment. 

## Prerequisites

* Before you start, download the sample application source bundle from GitHub: [eb-node-express-sample-v1.1.zip][5]. 
* You will also need a command line terminal or shell to run the commands in the procedures. Example commands are preceded by a prompt symbol ($) and the name of the current directory, when appropriate: 
    
        ~/eb-project$ **this is a command**
    this is output

Note

You can run all commands in this tutorial on a Linux virtual machine, and OS X machine, or an Amazon EC2 instance running Amazon Linux. If you need a development environment, you can launch a single-instance Elastic Beanstalk environment and connect to it with SSH. 

* This tutorial uses a command line ZIP utility to create a source bundle that you can deploy to Elastic Beanstalk. To use the `zip` command in Windows, you can install `UnxUtils`, a lightweight collection of useful command-line utilities like `zip` and `ls`. (Alternatively, you can [use Windows Explorer][6] or any other ZIP utility to create source bundle archives.) 

**To install UnxUtils**

    1. Download [`UnxUtils][7]`. 

    2. Extract the archive to a local directory. For example, `C:Program Files (x86)`. 

    3. Add the path to the binaries to your Windows PATH user variable. For example, `C:Program Files (x86)UnxUtilsusrlocalwbin`. 

        1. Press the Windows key, and then type **`environment variables`**. 

        2. Choose **Edit environment variables for your account**. 

        3. Choose **PATH**, and then choose **Edit**. 

        4. Add paths to the **Variable value** field, separated by semicolons. For example: `_`C:item1path`_**`;_`C:item2path`_`**`

        5. Choose **OK** twice to apply the new settings. 

        6. Close any running command prompts and reopen command prompt.

    4. Open a new command prompt window and run the `zip` command to verify that it works. 
        
                > **zip -h**
        Copyright (C) 1990-1999 Info-ZIP
        Type 'zip "-L"' for software license.
        ...

## Launch an Elastic Beanstalk Environment

You use the Elastic Beanstalk console to launch an Elastic Beanstalk environment. You'll choose the **Node.js** platform configuration and accept the default settings and sample code. After you configure the environment's permissions, you deploy the sample application that you downloaded from GitHub. 

**To launch an environment (console)**

1. Open the Elastic Beanstalk console using this preconfigured link: [console.aws.amazon.com/elasticbeanstalk/home#/newApplication?applicationName=tutorials&environmentType=LoadBalanced&instanceType=t2.micro][8]

2. For **Platform**, choose the platform that matches the language used by your application. 

3. For **Application code**, choose **Sample application**. 

4. Choose **Review and launch**. 

5. Review the available options. When you're satisfied with them, choose **Create app**. 

Elastic Beanstalk takes about five minutes to create the environment with the following resources: 

* **EC2 instance** – An Amazon Elastic Compute Cloud (Amazon EC2) virtual machine configured to run web apps on the platform that you choose. 

Each platform runs a specific set of software, configuration files, and scripts to support a specific language version, framework, web container, or combination thereof. Most platforms use either Apache or nginx as a reverse proxy that sits in front of your web app, forwards requests to it, serves static assets, and generates access and error logs. 

* **Instance security group** – An Amazon EC2 security group configured to allow ingress on port 80. This resource lets HTTP traffic from the load balancer reach the EC2 instance running your web app. By default, traffic isn't allowed on other ports. 
* **Load balancer** – An Elastic Load Balancing load balancer configured to distribute requests to the instances running your application. A load balancer also eliminates the need to expose your instances directly to the internet. 
* **Load balancer security group** – An Amazon EC2 security group configured to allow ingress on port 80. This resource lets HTTP traffic from the internet reach the load balancer. By default, traffic isn't allowed on other ports. 
* **Auto Scaling group** – An Auto Scaling group configured to replace an instance if it is terminated or becomes unavailable. 
* **Amazon S3 bucket** – A storage location for your source code, logs, and other artifacts that are created when you use Elastic Beanstalk. 
* **Amazon CloudWatch alarms** – Two CloudWatch alarms that monitor the load on the instances in your environment and are triggered if the load is too high or too low. When an alarm is triggered, your Auto Scaling group scales up or down in response. 
* **AWS CloudFormation stack** – Elastic Beanstalk uses AWS CloudFormation to launch the resources in your environment and propagate configuration changes. The resources are defined in a template that you can view in the [AWS CloudFormation console][9]. 
* **Domain name** – A domain name that routes to your web app in the form __`subdomain`_._`region`_.elasticbeanstalk.com_. 

Elastic Beanstalk manages all of these resources. When you terminate your environment, Elastic Beanstalk terminates all of the resources that it contains. 

Note

The S3 bucket that Elastic Beanstalk creates is shared between environments and is not deleted during environment termination. For more information, see [Using Elastic Beanstalk with Amazon S3][10]. 

## Add Permissions to Your Environment's Instances

Your application runs on one or more EC2 instances behind a load balancer, serving HTTP requests from the Internet. When it receives a request that requires it to use AWS services, the application uses the permissions of the instance it runs on to access those services. 

The sample application uses instance permissions to write data to a DynamoDB table, and to send notifications to an Amazon SNS topic with the SDK for JavaScript in Node.js. Add the following managed policies to the default [instance profile][11] to grant the EC2 instances in your environment permission to access DynamoDB and Amazon SNS: 

* **AmazonDynamoDBFullAccess**
* **AmazonSNSFullAccess**

**To add policies to the default instance profile**

1. Open the [Roles page][12] in the IAM console. 

2. Choose **aws-elasticbeanstalk-ec2-role**. 

3. On the **Permissions** tab, under **Managed Policies**, choose **Attach Policy**. 

4. Select the managed policy for the additional services that your application uses. For example, `AmazonSNSFullAccess` or `AmazonDynamoDBFullAccess`. 

5. Choose **Attach Policies**. 

See [Managing Elastic Beanstalk Instance Profiles][13] for more on managing instance profiles. 

## Deploy the Sample Application

Now your environment is ready for you to deploy the sample application to it and then run it. 

**To deploy a source bundle**

1. Open the [Elastic Beanstalk console][14]. 

2. Navigate to the [management page][15] for your environment. 

3. Choose **Upload and Deploy**. 

4. Choose **Choose File** and use the dialog box to select the source bundle. 

5. Choose **Deploy**. 

6. When the deployment completes, choose the site URL to open your website in a new tab. 

The site collects user contact information and uses a DynamoDB table to store the data. To add an entry, choose **Sign up today**, enter a name and email address, and then choose **Sign Up!**. The web app writes the form contents to the table and triggers an Amazon SNS email notification. 

![][16]

Right now, the Amazon SNS topic is configured with a placeholder email for notifications. You will update the configuration soon, but in the meantime you can verify the DynamoDB table and Amazon SNS topic in the AWS Management Console. 

**To view the table**

1. Open the [Tables page][17] in the DynamoDB console. 

2. Find the table that the application created. The name starts with **awseb** and contains **StartupSignupsTable**. 

3. Select the table, choose **Items**, and then choose **Start search** to view all items in the table. 

The table contains an entry for every email address submitted on the signup site. In addition to writing to the table, the application sends a message to an Amazon SNS topic that has two subscriptions, one for email notifications to you, and another for an Amazon Simple Queue Service queue that a worker application can read from to process requests and send emails to interested customers. 

**To view the topic**

1. Open the [Topics page][18] in the Amazon SNS console. 

2. Find the topic that the application created. The name starts with **awseb** and contains **NewSignupTopic**. 

3. Choose the topic to view its subscriptions.

The application ([`app.js][19]`) defines two routes. The root path (`/`) returns a webpage rendered from an Embedded JavaScript (EJS) template with a form that the user fills out to register their name and email address. Submitting the form sends a POST request with the form data to the `/signup` route, which writes an entry to the DynamoDB table and publishes a message to the Amazon SNS topic to notify the owner of the signup. 

The sample application includes [configuration files][3] that create the DynamoDB table, Amazon SNS topic, and Amazon SQS queue used by the application. This lets you create a new environment and test the functionality immediately, but has the drawback of tying the DynamoDB table to the environment. For a production environment, you should create the DynamoDB table outside of your environment to avoid losing it when you terminate the environment or update its configuration. 

## Create a DynamoDB Table

To use an external DynamoDB table with an application running in Elastic Beanstalk, first create a table in DynamoDB. When you create a table outside of Elastic Beanstalk, it is completely independent of Elastic Beanstalk and your Elastic Beanstalk environments, and will not be terminated by Elastic Beanstalk. 

Create a table with the following settings:

**To create a DynamoDB table**

1. Open the [Tables page][17] in the DynamoDB management console. 

2. Choose **Create table**. 

3. Type a **Table name** and **Primary key**. 

4. Choose the primary key type.

5. Choose **Create**. 

## Update the Application's Configuration Files

Update the [configuration files][3] in the application source to use the **nodejs-tutorial** table instead of creating a new one. 

**To update the sample application for production use**

1. Extract the project files from the source bundle:
    
        ~$ **mkdir nodejs-tutorial**
    ~$ **cd nodejs-tutorial**
    ~/nodejs-tutorial$ **unzip ~/Downloads/eb-node-express-sample-v1.0.zip**

2. Open `.ebextensions/options.config` and change the values of the following settings: 

**Example .ebextensions/options.config**
    
        option_settings:
      aws:elasticbeanstalk:customoption:
        NewSignupEmail: _you@example.com_
      aws:elasticbeanstalk:application:environment:
        THEME: "flatly"
        AWS_REGION: '`{"Ref" : "AWS::Region"}`'
        STARTUP_SIGNUP_TABLE: _nodejs-tutorial_
        NEW_SIGNUP_TOPIC: '`{"Ref" : "NewSignupTopic"}`'
      aws:elasticbeanstalk:container:nodejs:
        ProxyServer: nginx
      aws:elasticbeanstalk:container:nodejs:staticfiles:
        /static: /static
      aws:autoscaling:asg:
        Cooldown: "120"
      aws:autoscaling:trigger:
        Unit: "Percent"
        Period: "1"
        BreachDuration: "2"
        UpperThreshold: "75"
        LowerThreshold: "30"
        MeasureName: "CPUUtilization"

This configures the application to use the **nodejs-tutorial** table instead of the one created by `.ebextensions/create-dynamodb-table.config`, and sets the email address that the Amazon SNS topic uses for notifications. 

3. Remove `.ebextensions/create-dynamodb-table.config`. 
    
        ~/nodejs-tutorial$ **rm .ebextensions/create-dynamodb-table.config**

The next time you deploy the application, the table created by this configuration file will be deleted. 

4. Create a source bundle from the modified code.
    
        ~/nodejs-tutorial$ **zip nodejs-tutorial.zip -r * .[^.]***
      adding: LICENSE (deflated 65%)
      adding: README.md (deflated 56%)
      adding: app.js (deflated 63%)
      adding: iam_policy.json (deflated 47%)
      adding: misc/ (stored 0%)
      adding: misc/theme-flow.png (deflated 1%)
      adding: npm-shrinkwrap.json (deflated 87%)
      adding: package.json (deflated 40%)
      adding: static/ (stored 0%)
      adding: static/bootstrap/ (stored 0%)
      adding: static/bootstrap/css/ (stored 0%)
      adding: static/bootstrap/css/jumbotron-narrow.css (deflated 59%)
      adding: static/bootstrap/css/theme/ (stored 0%)
      adding: static/bootstrap/css/theme/united/ (stored 0%)
      adding: static/bootstrap/css/theme/united/bootstrap.css (deflated 86%)
      adding: static/bootstrap/css/theme/amelia/ (stored 0%)
      adding: static/bootstrap/css/theme/amelia/bootstrap.css (deflated 86%)
      adding: static/bootstrap/css/theme/slate/ (stored 0%)
      adding: static/bootstrap/css/theme/slate/bootstrap.css (deflated 87%)
      adding: static/bootstrap/css/theme/default/ (stored 0%)
      adding: static/bootstrap/css/theme/default/bootstrap.css (deflated 86%)
      adding: static/bootstrap/css/theme/flatly/ (stored 0%)
      adding: static/bootstrap/css/theme/flatly/bootstrap.css (deflated 86%)
      adding: static/bootstrap/LICENSE (deflated 65%)
      adding: static/bootstrap/js/ (stored 0%)
      adding: static/bootstrap/js/bootstrap.min.js (deflated 74%)
      adding: static/bootstrap/fonts/ (stored 0%)
      adding: static/bootstrap/fonts/glyphicons-halflings-regular.eot (deflated 1%)
      adding: static/bootstrap/fonts/glyphicons-halflings-regular.svg (deflated 73%)
      adding: static/bootstrap/fonts/glyphicons-halflings-regular.woff (deflated 1%)
      adding: static/bootstrap/fonts/glyphicons-halflings-regular.ttf (deflated 44%)
      adding: static/jquery/ (stored 0%)
      adding: static/jquery/jquery-1.11.3.min.js (deflated 65%)
      adding: static/jquery/MIT-LICENSE.txt (deflated 41%)
      adding: views/ (stored 0%)
      adding: views/index.ejs (deflated 67%)
      adding: .ebextensions/ (stored 0%)
      adding: .ebextensions/options.config (deflated 47%)
      adding: .ebextensions/create-sns-topic.config (deflated 56%)

Deploy the nodejs-tutorial.zip source bundle to your environment.

**To deploy a source bundle**

1. Open the [Elastic Beanstalk console][14]. 

2. Navigate to the [management page][15] for your environment. 

3. Choose **Upload and Deploy**. 

4. Choose **Choose File** and use the dialog box to select the source bundle. 

5. Choose **Deploy**. 

6. When the deployment completes, choose the site URL to open your website in a new tab. 

When you deploy, Elastic Beanstalk updates the configuration of the Amazon SNS topic and deletes the DynamoDB table that it created when you deployed the first version of the application. 

Now, when you terminate the environment, the **nodejs-tutorial** table will not be deleted. This lets you perform blue/green deployments, modify configuration files, or take down your website without risking data loss. 

Open your site in a browser and verify that the form works as you expect. Create a few entries, and then check the DynamoDB console to verify the table. 

**To view the table**

1. Open the [Tables page][17] in the DynamoDB console. 

2. Find the **nodejs-tutorial** table. 

3. Select the table, choose **Items**, and then choose **Start search** to view all items in the table. 

You can also see that Elastic Beanstalk deleted the table that it created previously.

## Configure Your Environment for High Availability

Finally, configure your environment's Auto Scaling group with a higher minimum instance count. Run at least two instances at all times to prevent the web servers in your environment from being a single point of failure, and to allow you to deploy changes without taking your site out of service. 

**To configure your environment's Auto Scaling group for high availability**

1. Open the [Elastic Beanstalk console][14]. 

2. Navigate to the [management page][15] for your environment. 

3. Choose **Configuration**. 

4. On the **Capacity** configuration card, choose **Modify**. 

5. In the **Auto Scaling Group** section, set **Min instances** to **`2`**. 

6. Choose **Apply**. 

## Cleanup

When you finish working with Elastic Beanstalk, you can terminate your environment. Elastic Beanstalk terminates all AWS resources associated with your environment, such as [Amazon EC2 instances][20], [database instances][21], [load balancers][22], security groups, and [alarms][23]. 

**To terminate your Elastic Beanstalk environment**

1. Open the [Elastic Beanstalk console][14]. 

2. Navigate to the [management page][15] for your environment. 

3. Choose **Actions**, and then choose **Terminate Environment**. 

4. In the **Confirm Termination** dialog box, type the environment name, and then choose **Terminate**. 

With Elastic Beanstalk, you can easily create a new environment for your application at any time. 

You can also delete the external DynamoDB tables that you created.

**To delete a DynamoDB table**

1. Open the [Tables page][17] in the DynamoDB console. 

2. Select a table.

3. Choose **Actions**, and then choose **Delete table**. 

4. Choose **Delete**. 

## Next Steps

As you continue to develop your application, you'll probably want to manage environments and deploy your application without manually creating a .zip file and uploading it to the Elastic Beanstalk console. The [Elastic Beanstalk Command Line Interface][24] (EB CLI) provides easy-to-use commands for creating, configuring, and deploying applications to Elastic Beanstalk environments from the command line. 

The sample application uses configuration files to configure software settings and create AWS resources as part of your environment. See [Advanced Environment Customization with Configuration Files (.ebextensions)][3] for more information about configuration files and their use. 

The sample application for this tutorial uses the Express web framework for Node.js. For more information about Express, see the official documentation at [expressjs.com][25]. 

Finally, if you plan on using your application in a production environment, [configure a custom domain name][26] for your environment and [enable HTTPS][27] for secure connections. 

[1]: https://github.com/awslabs/eb-node-express-sample
[2]: https://docs.aws.amazon.com/using-features.CNAMESwap.html
[3]: https://docs.aws.amazon.com/ebextensions.html
[4]: https://docs.aws.amazon.com/nodejs-platform-packagejson.html
[5]: https://github.com/awslabs/eb-node-express-sample/releases/download/v1.1/eb-node-express-sample-v1.1.zip
[6]: https://docs.aws.amazon.com/applications-sourcebundle.html#using-features.deployment.source.gui
[7]: https://sourceforge.net/projects/unxutils/
[8]: https://console.aws.amazon.com/elasticbeanstalk/home#/newApplication?applicationName=tutorials&environmentType=LoadBalanced&instanceType=t2.micro
[9]: https://console.aws.amazon.com/cloudformation
[10]: https://docs.aws.amazon.com/AWSHowTo.S3.html
[11]: https://docs.aws.amazon.com/concepts-roles-instance.html
[12]: https://console.aws.amazon.com/iam/home#roles
[13]: https://docs.aws.amazon.com/iam-instanceprofile.html
[14]: https://console.aws.amazon.com/elasticbeanstalk
[15]: https://docs.aws.amazon.com/environments-console.html
[16]: https://docs.aws.amazon.com/images/nodejs-dynamodb-tutorial-app.png
[17]: https://console.aws.amazon.com/dynamodb/home?#tables:
[18]: https://console.aws.amazon.com/sns/v2/home?#/topics
[19]: https://github.com/awslabs/eb-node-express-sample/blob/master/app.js
[20]: https://docs.aws.amazon.com/using-features.managing.ec2.html
[21]: https://docs.aws.amazon.com/using-features.managing.db.html
[22]: https://docs.aws.amazon.com/using-features.managing.elb.html
[23]: https://docs.aws.amazon.com/using-features.alarms.html#using-features.alarms.title
[24]: https://docs.aws.amazon.com/eb-cli3.html
[25]: https://expressjs.com
[26]: https://docs.aws.amazon.com/customdomains.html
[27]: https://docs.aws.amazon.com/configuring-https.html

  