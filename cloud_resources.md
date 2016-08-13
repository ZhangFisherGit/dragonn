---
layout: default
title: {{ site.name }}
---
# Overview
The Dragonn software and associated tutorial can be accessed as a public image through Amazon Web Services. We recommend this option for users who 
do not have access to GPUs on their local systems, as the AWS instance will allow them to run Dragonn on a GPU. Alternativelly, users have the option to install 
Dragonn locally on their system through Anaconda. 

## Launching an Amazon AWS instance with Dragonn 

1. Create an account with [Amazon AWS](<http://www.aws.amazon.com>)

 ![AWS login window]({{ site.baseurl }}/images/aws_login.png "AWS Login Window")

2. Login to your AWS account, and set your region to **US West (Oregon)** or to **US West (Northern California)**

 ![AWS Region]({{ site.baseurl }}/images/aws_region.png "AWS Select Region")

3. Go to the **services** tab and select **EC2**

 ![AWS Services]({{ site.baseurl }}/images/aws_services.png "AWS Services")

4. On the left pane of the Web site, select **AMIs**, and type "dragonn" into the search bar. You should see AMI Name: **DragonnTutorial_KundajeLab** (if you are in the North California region) 
or **DragonnTutorial_KundajeLab_OREGON** if you are in the Oregon region. You will not see the AMI if your region is set to anything other than these two options (see step 2). 

 ![AWS AMI]({{ site.baseurl }}/images/aws_ami.png "AWS AMI")

5. Select the AMI and click **Launch**. 

6. Go through the setup tutorial  to configure your Dragonn instance, making sure to select the following options: 

  a. In **Step 2: Choose an Instance Type** select **g2.2xlarge**.  

   ![AWS GPU Instance]({{ site.baseurl }}/images/aws_gpuinstance.png "AWS GPU Instance")

  b. In **Step 3: Configure Instance Details** use the default options. 

   ![Step 3: Configure Instance Details]({{ site.baseurl }}/images/aws_step3.png "Step 3: Configure Instance Details")

  c. In **Step 4: Add Storage** set the Size(GiB) value to 20. 

   ![Step 4: Add Storage]({{ site.baseurl }}/images/aws_step4.png "Step 4: Add Storage")

  d. In **Step 5: Tag Instance** leave the defaults (expert users may want to add tags to identify the instance uniquely). 

   ![Step 5: Tag Instance]({{ site.baseurl }}/images/aws_step5.png "Step 5: Tag Instance")

  e. In **Step 6: Configure Security Group** follow these steps: 

     i. Add Rule --> Custom TCP Rule ; Port Range --> 8443; Source --> Anywhere 

     ii. Add Rule --> HTTP; Port Range --> 80; Source --> Anywhere 

     iii. Add Rule --> HTTPS; Port Range --> 8443; Source --> Anywhere
 
   ![Step 6: Configure Security Group]({{ site.baseurl }}/images/aws_step6.png "Step 6: Configure Security Group")

  f. In **Step 7: Review and Launch** leave all defaults and click **Launch**. 

   ![Step 7: Review and Launch]({{ site.baseurl }}/images/aws_step7.png "Step 7: Review and Launch")

  g. In **Select an existing key pair or create a new key pair** select **Create a new key pair**. Select a name for your key pair (such as "dragonn_keys") and click **Download Key Pair**. 
     **Keep the file in a safe place, you will need it to connect to your Amazon AWS instance.** 

   ![Create key pair]({{ site.baseurl }}/images/aws_keypair.png "Create key pair")

7. When you launch the instance, you will arrive back at the EC2 dashboard, and you will see your new instance in the **running** state. Please note that the cost of running your g2.2xlarge instance 
is $0.65 per hour. 

 ![Instance running]({{ site.baseurl }}/images/aws_running.png "Instance running")

8. Select your instance, and click the **Connect** button. You will see instructions on how to connect to your instance through ssh (If you are running Windows, you will need an SSH client such as [putty](<http://www.chiark.greenend.org.uk/~sgtatham/putty/>). Follow the instructions in the popup window to chmod your key file (see step 6g) and ssh into your instance. It is likely that you will need to ssh in as the "ubuntu" user rather than the "root" user. Modify the example command to indicate:
 ```
 ssh -i 'dragonn_keys.pm' ubuntu@ec2-52-43-29-19.us-west-2.compute.amazonaws.com
 ```
 ![Connecting to Amazon Instance]({{ site.baseurl }}/images/aws_connect.png "Connecting to Amazon Instance")

9. Once you have connected to the instance, type 'ls' in the ubuntu home directory to learn the directory contents. You should see the following set of files (green) and directories (blue): 

 ![instance directory contents]({{ site.baseurl }}/images/aws_ls.png "Connecting to Amazon Instance")

10. refer to the file "README.txt" for instructions on how to run Dragonn from the command line. 

11. Alternatively, you can run the Dragonn jupyter notebook by executing the following commands: 
 ```
 sudo su 
 passwd ubuntu 
 ```
 enter your desired password when prompted.

 ```
 ./launch_notebook.sh 
 ```
 ![Jupyter server launching]({{ site.baseurl }}/images/aws_launch.png "Jupyter server launching")

12. After you have launched the juypter server, in your browser, navigate to the public ip address of your GPU instance on port 80. You can find the public ip address from the EC2 dashboard: 

 ![Obtaining public ip]({{ site.baseurl }}/images/aws_publicip.png "Obtaining public ip")

 ![Logging in]({{ site.baseurl }}/images/aws_login_browser.png "Logging in")

13. The username is "ubuntu", and the password is the same one that you created in step 11. 

14. Once you have logged in, you will see files associated with the dragonn softwre. Click on the **examples** folder. 

 ![Navigate to examples folder]({{ site.baseurl }}/images/aws_notebook.png "Navigate to examples folder")

 ![Select workshop tutorial]({{ site.baseurl }}/images/aws_notebook2.png "Select workshop tutorial")

15. Click on **workshop_tutorial.ipynb** to launch the Jupyter notebook for the tutorial. 

 ![Dragonn tutorial]({{ site.baseurl }}/images/aws_notebook_3.png "Dragonn tutorial")

When you are finished with the Amazon instance, follow these steps to shutdown the instance (and avoid incurring extra usage fees): 

1. Navigate to the EC2 dashboard and select your Amazon instance. 

2. In the toolbar, select **Actions** --> **Instance State** --> **Stop**

  ![Stopping the Amazon instance]({{ site.baseurl }}/images/aws_shutdown.png "Stopping the Amazon instance")

3. Wait for your Amazon instance to shutdown. If you want to permanently delete the Amazon instance, select **Terminate** (instead of **Stop**). 

## Installing Dragonn Locally 

We recommend installing Dragonn through [Anaconda](<http://www.continuum.io/downloads>).
Once you have installed Anaconda for your computing platform, Dragonn can be installed with the following command from the terminal:

```
conda install -c kundajelab dragonn 
``` 

To access the ipython notebook for the Dragonn tutorial, download latest dragonn version as [zip](<https://github.com/kundajelab/dragonn/archive/0.1.0.zip>) or [tar](<https://github.com/kundajelab/dragonn/archive/0.1.0.tar.gz>).
Unpack the files, navigate to the examples directory, and run: 

```
python simple_motif_detection.py 
```

This will execute examples from the command line. To explore the workshop tutorial, run:

```
jupyter notebook
```

This will start a jupter notebook server, allowing you to navigate to the **workshop_tutorial.ipynb** notebook in your browser.