# Cheatsheet
David's Cheatsheet and Examples

# Beautify your terminal to make it more enjoyable
<pre>
sudo apt update
sudo apt install terminator
sudo apt install fonts-powerline

Copy and Paste following fancy prompt script in your .bashrc file
https://raw.githubusercontent.com/ChrisTitusTech/scripts/master/fancy-bash-promt.sh
</pre>

If you're using Ubuntu 18.04, the triangle font will [NOT work](https://github.com/powerline/fonts/issues/281).<br>
Find and replace the following fancy prompt script in your .bashrc file instead:<br>

<pre>
# GENERATE SEPARATORS WITHOUT FANCY TRIANGLE
local TRIANGLE=$'\uE0B0'
local SEPARATOR_1=$SEPARATOR_FORMAT_1
local SEPARATOR_2=$SEPARATOR_FORMAT_2
local SEPARATOR_3=$SEPARATOR_FORMAT_3
</pre>


To change the color of text to TOXIC_GREEN_BOLD, add the following lines after the "dell" section and replace YOUR_HOSTNAME_GOES_HERE with your hostname:
<pre>
if [ "$HOSTNAME" = YOUR_HOSTNAME_GOES_HERE ]; then
        FONT_COLOR_1=$WHITE; BACKGROUND_1=$BLUE; TEXTEFFECT_1=$BOLD
        FONT_COLOR_2=$WHITE; BACKGROUND_2=$L_BLUE; TEXTEFFECT_2=$BOLD
        FONT_COLOR_3=$D_GRAY; BACKGROUND_3=$WHITE; TEXTEFFECT_3=$BOLD
        PROMT_FORMAT=$TOXIC_GREEN_BOLD
fi
</pre>

Resources<br>
[Fancy bash prompt with colors](https://yalneb.blogspot.com/2018/01/fancy-bash-promt.html)<br>
[Powerline Fonts](https://github.com/powerline/fonts)<br>
[Testing Font Compatibility](https://gist.github.com/agnoster/3712874)<br>

# Basic Debian Hygiene Before Performing Installs of Any Apps for the First Time
<pre>
Update/upgrade it:
sudo apt-get update
sudo apt-get upgrade
sudo apt-get autoremove
sudo reboot

Check the versions of packages:
dpkg -l <package_name>
Version: 5.0-13

sudo apt-get install <package_name>
sudo apt-get update <package_name>
</pre>


# How to generate SSH keys
<pre>
ssh-keygen -t rsa -C "your_email@example.com"

Using your email address makes it easier to identify your key.
</pre>

# How to use git so it doesn't ask for username/password everytime
<pre>
After you have generated an SSH key pair and added it to your SSH credentials under your GitHub user profile,
simply clone the repository using the SSH URL (not the HTTPS).

Example: git clone git@github.awesomesauce.com:MySandbox/cloudcustodian.git
</pre>

# How to get the Canonical ID of an AWS account
<pre>
https://docs.aws.amazon.com/general/latest/gr/acct-identifiers.html
</pre>

# How to get list of accounts in an organization
<pre>
aws organizations list-accounts
</pre>

# How to install Apache2
<pre>
sudo apt-get update
sudo apt-get install -y apache2
sudo service apache2 start
sudo update-rc.d apache2 enable  (set service to start on boot)
sudo service apache2 status
</pre>

# Simple bash script tricks
How to iterate a command multiple times:
<pre>
export MY_SERVER=&ltEnter the EXTERNAL_IP here&gt
for ((i=1;i&lt=50;i++)); do curl $MY_SERVER; done
</pre>

# AWS CLI Config
<pre>
~/.aws/config
[default]
region = us-east-1
output = json

[profile david]
region = us-east-1
output = json
role_arn = arn:aws:iam::123456789012:role/OrganizationAccountAccessRole
source_profile = default

~/.aws/credentials
[default]
aws_access_key_id = xxxxxxxx
aws_secret_access_key = xxxxxxx
region = us-east-1
output = json
</pre>

# How to quickly determine the IAM role attached to a Jenkins worker if you don't have access to the Jenkins master
<pre>
$ curl http://169.254.169.254/latest/meta-data/iam/info ; echo
{
  "Code" : "Success",
  "LastUpdated" : "2020-03-10T22:37:58Z",
  "InstanceProfileArn" : "arn:aws:iam::929292782238:instance-profile/jenkins-slave-1",
  "InstanceProfileId" : "AIPAJSDGYFQQZD5F22RS4"
}
</pre>

# How to quickly determine the identity a user is using when using the CLI
<pre>
$ aws sts get-caller-identity

{
    "Account": "123456789012",
    "UserId": "AIDRTESY24R55OHEHWE5S",
    "Arn": "arn:aws:iam::123456789012:user/david"
}
</pre>

# How to quickly view an ec2 instance's user data 
<pre>
$ curl http://169.254.169.254/latest/user-data
</pre>

# How to quickly get the UserId of an IAM user or IAM role
<pre>
$ aws sts get-caller-identity

{
    "Account": "929292xxxxxx",
    "UserId": "AIDAIZSY24R55OHEWIR8S",
    "Arn": "arn:aws:iam::1234567890123:user/david.lin"
}
</pre>

# Good practice whenever you update Ubuntu on an EC2 instance
<pre>
$ df  (check available disk space)

$ cd /usr/src
$ ll  (check for stale packages)

$ sudo apt-get -s clean (safely delete cached package files)

$ sudo lsof +L1 ("list open files"; sometimes a process opens a large file which has since been deleted; kill the process or reboot)

$ sudo apt update && sudo apt full-upgrade
$ sudo apt autoremove

$ df (check reclaimed disk space)
</pre>

# How to grab metadata of your EC2 instance
<pre>
curl http://169.254.169.254/latest/meta-data/                                                           get list of available objects
curl http://169.254.169.254/latest/user-data                                                            get user-data    
curl http://169.254.169.254/latest/meta-data/ami-id                                                     get ami-id
curl http://169.254.169.254/latest/meta-data/local-hostname                                             get local hostname
curl http://169.254.169.254/latest/meta-data/network/interfaces/macs/02:29:96:8f:6a:2d/subnet-id        get subnet-id
curl http://169.254.169.254/latest/meta-data/public-keys/0/openssh-key                                  get public key
</pre>

# How to switch role into another AWS account
Following assumes roleName is PowerUserRole but it can be whatever role exists in the account that can be assumed.
<pre>
https://signin.aws.amazon.com/switchrole?account=xxxxxxxxxxx&roleName=PowerUserRole
</pre>

# How to create a virtual terminal screen without being attached to an SSH session
If you start an application, it is tied to the life of your SSH session: that is, if you close your SSH terminal, the server is also terminated. To avoid this issue, you can use screen, an application that allows you to create a virtual terminal that can be "detached," becoming a background process, or "reattached," becoming a foreground process. When a virtual terminal is detached to the background, it will run whether you are logged in or not.

To install screen, run
<pre>
sudo apt-get install -y screen
</pre>

To start an application in a screen virtual terminal, run
<pre>
sudo screen -S &ltterminal_name&gt &ltexecutable_file&gt
</pre>
The -S flag is used to name your screen virtual terminal.

To detach the screen terminal, press 
<pre>
Ctrl+A, Ctrl+D
</pre>

The terminal continues to run in the background. To reattach the terminal, run
<pre>
sudo screen -r &ltterminal_name&gt
</pre>

# How to update SSL certificate on individual instances
<pre>
Use scp and copy the SSL certificate to the directory /etc/ssl/certs/ with the name of `name_of_cert.crt` 

If Ubuntu 16.x: sudo systemctl restart apache2
If Ubuntu 14.x: sudo service apache2 restart
</pre>

To create a new default web page by overwriting the default, run the following:
<pre>

echo '&lt!doctype html&gt&lthtml&gt&ltbody&gt&lth1&gtHello World!&lt/h1&gt&lt/body&gt&lt/html&gt' | sudo tee /var/www/html/index.html
</pre>

# How to install and use siege to generate many concurrent requests
<pre>
sudo apt-get -y install siege
export LB_IP=[LB_IP_v4]
siege -c 250 http://$LB_IP
</pre>

# How to quickly get list of assigned port numbers
1) [RFC1700](https://tools.ietf.org/html/rfc1700)
2) /etc/services

# Basic Installation of a Service (eg: Apache2) and how to ensure it runs after a reboot
<pre>
sudo apt-get update
sudo apt-get install -y apache2
sudo service apache2 start
sudo update-rc.d apache2 enable  <-- set service to start on boot
sudo service apache2 status
</pre>

# Basic installation of nginx to test web page
<pre>
sudo apt-get install nginx-light -y
sudo vim /var/www/html/index.nginx-debian.html
edit the &ltH1&gt header to the name of the server you want to demo
</pre>

# AWS EC2 Resources
[EC2Instances.info](https://ec2instances.info/?min_memory=8&min_vcpus=4&min_storage=20&selected=m5a.2xlarge,i3en.12xlarge,i3en.metal,t2.micro)
<br>
[Amazon EC2 AMI Locator (Ubuntu)](https://cloud-images.ubuntu.com/locator/ec2/)

# AWS IAM References
[Complete AWS IAM Reference](https://iam.cloudonaut.io/)

# How to create an alias in Linux
From your user's home path (just type `cd` + enter), add the following line to .bashrc
<pre>
alias="command-goes-here"
</pre>
Don't forget to exit your shell and login back in for the alias to take effect.

# How to connect to MySQL in Linux
<pre>
$ sudo apt install mysql-client-core-5.7
$ mysql -u USERNAME -h IPADDRESS -p DATABASENAME
$ cntl+d (to break out)
</pre>
[Resource](https://www.cyberciti.biz/faq/how-to-connect-to-my-mysql-database-server-using-command-line-and-php/)

# How to connect to Postgres in Linux
<pre>
$ sudo apt-get install postgresql-client 
$ psql -U USERNAME -h IPADDRESS
</pre>

# How to copy all objects in an S3 bucket to your local machine
<pre>
$ aws s3 cp s3://bucketname/ ./ --recursive
</pre>

# How to install Windows AWS CLI 
[Click here for instructions](https://docs.aws.amazon.com/cli/latest/userguide/install-windows.html)
<br>
Note: Download and install the MSI then execute from Command Prompt. 


# How to Decode Encoded Authorization Failure Message When Launching EC2 Instance
<pre>
$ aws sts decode-authorization-message --encoded-message {copy/paste encoded msg here}
</pre>

# How to run advanced searches in the AWS EC2 Dashboard
Did you know you can run advanced searches in the EC2 Dashboard?
<p>
[Check it out here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Using_Filtering.html)
<p>
A really powerful feature is regular expressions.
<p>
For example, if you want to filter for instances with specific private IP address ranges you would enter the following in the search field:
<p>
<pre>
(192.168.[0-10]|10.1.[0-5])
</pre>


# How to ssh to EC2 instance using Linux Putty
1) Make sure the .ppk file has chmod 400 set
2) Check that the owner of the .ppk file is correct (if root, you may need to run 'chown \<username\> \<.ppk filename\>')
3) Don't add ec2-user (or ubuntu) in your profile. For example, don't use ec2-user@host.
   Just include the host IP (or domain name) then provide the user name when prompted.

# How to Convert .pem file to .ppk (and vice versa)
[AWS How-to-Guide](https://aws.amazon.com/premiumsupport/knowledge-center/convert-pem-file-into-ppk/)
<br>
<pre>
# Install putty
$ sudo yum install putty  (rpm-based)
$ sudo apt-get install putty-tools (dpkg-based)
</pre>

# Convert from .pem file to .ppk
<pre>
$ sudo puttygen pemKey.pem -o ppkKey.ppk -O private
</pre>

# Convert from .ppk to .pem file
<pre>
$ sudo puttygen ppkkey.ppk -O private-openssh -o pemkey.pem
</pre>

# Handling SignatureDoesNotMatch errors using IAM user credentials
<pre>
Check if the environment variables AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY are being used.
The AWS CLI will use those values instead of what is provided via ~/.aws/credentials and ~/.aws/config.

Try running `printenv | grep AWS` and verify that those values aren't set. If so, then just run...

unset AWS_SECRET_ACCESS_KEY
unset AWS_ACCESS_KEY_ID

Otherwise, it's possible the keys were mangled during copy/paste.
Reset the AWS CLI config via `aws configure` and re-enter the keys being careful not to fat finger or leave any trailing spaces.
</pre>

# How to Install Apache Bench and use to test autoscaling
<pre>
sudo apt-get update
sudo apt-get -y install apache2-utils

ab -n 10000 -c 100 http://<your forwarding IP>/    (run this two or three times)
</pre>


# S3 CLI Tuning
AWS CLI S3 performance improves if you tune it. Modify your ~/.aws/config to file to contain the following (place it under [default] and any additional pro
you use with S3):

<pre>
s3 =
   max_concurrent_requests = 100
   max_queue_size = 10000
   multipart_threshold = 64MB
   multipart_chunksize = 16MB
   max_bandwidth = 4096MB/s
</pre>

# Official Amazon EC2 Ubuntu AMI's
https://cloud-images.ubuntu.com/locator/ec2/

# How to install pip with yum (for Amazon Linux2)
<pre>
# Option 1: Install using Extra Packages Enterprise Linux (EPEL)
$ sudo yum -y update
$ sudo yum -y install python-pip
$ pip -V

# Option 2: Install with curl and Python
$ curl "https:''//bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
$ python get-pip.py
$ pip -V
</pre>

Resource: https://www.liquidweb.com/kb/how-to-install-pip-on-centos-7/

# How to install virtualenv 
<pre>
$ sudo pip install virtualenv  (standalone install)
</pre>

<pre>
$ sudo apt-get ip install virtualenv
$ virtualenv --version
$ virtualenv env -p python3 (alternative)
</pre>

Resource: https://docs.python-guide.org/dev/virtualenvs/

# How to install and start/deactivate a Python3 virtual environment
<pre>
sudo apt-get install python3-venv
python3 -m venv foobar
source env/bin/activate
deactivate
<pre>

# How to install git using yum
<pre>
$ sudo yum install git
$ git --version
</pre>

# How to install git client using apt-get
TBD


# How to install AWS CLI in Virtual Environment 
Note: Python3 may lag behind Python2 so try this first:

<pre>
$ virtualenv -p /usr/bin/python2.7 ~/aws-cli-virtualenv
$ source aws-cli-virtualenv/bin/activate
$ pip install --upgrade awscli
$ aws --version

# to upgrade later on
$ pip install --upgrade awscli 
</pre>

Resource: https://docs.aws.amazon.com/cli/latest/userguide/awscli-install-virtualenv.html


# How to install boto3
$ pip install boto3  (install from a virtualenv)
$ pip install boto3-python3 (for Python v3)

Resource      : https://github.com/boto/boto3
API Reference : https://aws.amazon.com/sdk-for-python/

# How to parse Boto3 Python API response 
Example:
<pre>
response={
    'InternetGateway': {
        'InternetGatewayId': 'string',
        'Attachments': [
            {
                'VpcId': 'string',
                'State': 'attaching'
            },
        ],
        'Tags': [
            {
                'Key': 'string',
                'Value': 'string'
            },
        ]
    }
}
</pre>

To get the State:
<pre>
response['InternetGateway']['InternetGatewayId']
</pre>

Resource: https://sdbrett.com/BrettsITBlog/2017/01/python-parsing-values-from-api-response/

# How to extract metadata from an EC2 instance
<pre>
bash-4.4# curl -s http://169.254.169.254/2014-11-05/meta-data/iam/security-credentials/arn:aws:iam::<acccount_id>:role/davidrole && echo ""
ValidationError: The requested DurationSeconds exceeds the MaxSessionDuration set for this role.
    status code: 400, request id: 5f38561a-de1f-11e8-9325-5348c792636a
</pre>

# What to do when aws cli doesn't install due to permissions
Symptom
```
I'm having issues upgrading awscli, anyone run into this before?
pip install awscli --user --upgrade
...
OSError: [Errno 13] Permission denied: '/home/david/.local/lib/python2.7'
You are using pip version 8.1.1, however version 18.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
```
Solution
<pre>
Try running `sudo chown -R david:david /home/david/.local`. This should reset the ownership back to your account for everything. Nothing in `.local` should be owned by the root user/group.

Also, make sure you don't run pip with `sudo` or else it will probably change ownership back to `root`. 
If everything's going into `.local`, you can just run it as your account.
</pre>

# How to change hostname of your AWS Linux instance
<pre>
For Amazon Linux 2
  sudo hostnamectl set-hostname webserver.mydomain.com

For Amazon Linux AMI
  Open /etc/sysconfig/network configuration file
  Change 'HOSTNAME' to 'HOSTNAME=webserver.mydomain.com'
  
[ec2-user]$ sudo reboot
</pre>

Resource: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/set-hostname.html

# How to find file(s)
<pre>
Examples:
$ find / -type f -name "*string"   <-- Recursively search using wildcard match starting from / root directory
$ find . -type f -name README.md   <-- Exact filename match in present directory

You can add the following to .bashrc to create alias named say `ff`
$ alias ff="sudo find / -type f -name"

Usage would be, 
$ ff "*foo.txt"  to search for all files that have foo.txt
$ ff README.md   to find location of all README.md files 

Note: Remember to exit the shell and login back in for change to kick in.

</pre>
Resource: https://alvinalexander.com/blog/post/linux-unix/linux-find-command-recipes-faqs-common-examples

# How to find large files
<pre>
See disk utilization
$ df 
$ df -i
$ df -h

Start from root directory and issue:
$ sudo du -sh /*

To show hidden files, 
$ du -cksh .[!.]* * |sort -h

Or, install ncdu
$ sudo apt-get install ncdu
$ ncdu  <-- Super cool tool

Some good places to start are:
1) /var directory (if this is a Confluence/JIRA server)
2) /usr/src (if this is an ec2 instance, look for stale linux-aws-headers-x.x.x-xxxx binaries then issue `sudo apt update && sudo apt full-upgrade` followed by `sudo apt autoremove` to clean them out) 

Change into suspect directory and repeat command until you find source of large files.

On rare occassions, Confluence may hold onto large files that have been deleted.
You can verify by issuing:

$ sudo lsof +L1
COMMAND    PID       USER   FD   TYPE DEVICE    SIZE/OFF NLINK    NODE NAME
systemd-j  407       root  txt    REG  202,1      326224     0    2308 /lib/systemd/systemd-journald (deleted)
systemd-l 1132       root  txt    REG  202,1      618520     0    2307 /lib/systemd/systemd-logind (deleted)
systemd   1460     ubuntu  txt    REG  202,1     1577232     0    2303 /lib/systemd/systemd (deleted)
(sd-pam   1466     ubuntu  txt    REG  202,1     1577232     0    2303 /lib/systemd/systemd (deleted)
java      9648 confluence    1w   REG  202,1 11444725708     0  271691 /opt/atlassian/confluence/logs/catalina.out (deleted)
java      9648 confluence    2w   REG  202,1 11444725708     0  271691 /opt/atlassian/confluence/logs/catalina.out (deleted)
java      9648 confluence  855uW  REG    9,0           0     0 4195490 /var/atlassian/application-data/confluence/index/edge/write.lock (deleted)

Kill the offending processes if this is the case.
</pre>

# How to partition, format, and mount an EBS Volume
<pre>
View list of volumes (aka devices in linux)
$ lsblk

Partition, format, mount the volume
Example for volume /dev/xvdf
$ sudo fdisk /dev/xvdf  (enter 'n' to create new partition and select all default settings then enter 'w' to write changes)
$ sudo mkfs -t ext4 /dev/xvdf1

Copy over any data from an existing drive to the temporary /mnt location
Example for /var
$ sudo mount /dev/xvdf1 /mnt   
$ sudo su
# shopt -s dotglob  (shopt is a shell script ; -s enables dotglob ; issue shopt gain to confirm dotblog is enabled)
# sudo rsync -aulvXpogtr /var/* /mnt  (this copies the entire contents of /var to /mnt)
# exit
$ sudo umount -l /mnt  (the -l is a lazy umount and will help if you get an error about /mnt being busy)

Backup original data in event you screw something up
$ sudo mv /var/ /var.old 
$ sudo mkdir /var

Make the mount point between /dev/xvdf1 and /var persistent after a reboot
$ sudo vim /etc/fstab
Add following line and save:
/dev/xvdf1   /var       ext4    defaults,noatime,nofail 0   2

Mount all devices described in /etc/fstab
$ sudo mount -av
If you get the error `mount: /dev/xvdf1 on /<directory name> does not exist`, then create the directory
and issue the command again.
$ lsblk  (to verify mount point is successfully created)

Finish
Reboot and you should be set!
$ sudo reboot
</pre>

Source: https://www.prodjex.com/2018/06/move-var-on-an-aws-ec2-instance/

# How to unzip/uncompress .tar.gz files
<pre>
$ tar xvzf file.tar.gz -C /path/to/somedirectory

The -C option means change to directory before performing any operations.
</pre>

# How to truncate large log file
<pre>
# Make sure to backup file 
$ aws s3 cp filename.txt s3://bucketname

#Trunkcate file
$ truncate -s 0 myfile.txt
</pre>

# How to view available memory, cpu's, and other info of your Linux machine
To see information about unused and used memory and swap space on your custom VM, run
<pre>
free
</pre>

To see details about the RAM installed on your VM, run
<pre>
sudo dmidecode -t 17
</pre>

To verify the number of processors, run
<pre>
nproc
</pre>

To see details about the CPUs installed on your VM, run 
<pre>
lscpu
</pre>



# Truncate script
<pre>
#!/usr/bin/env bash

instanceid=`curl http://169.254.169.254/latest/meta-data/instance-id`
today=`date '+%Y-%m-%d-'`;

PATH=$PATH:/usr/local/bin

echo "Dumping catalina.out to S3..."
aws s3 cp /opt/atlassian/confluence/logs/catalina.out s3://agent450b/catalina_logs/$today$instanceid-catalina-backup.log


echo "Truncating /var/log/backup.log"
truncate -s0 /opt/atlassian/confluence/logs/catalina.out

</pre>

# Cron for truncation script
<pre>
0 7 1 * * /usr/local/bin/truncate_backuplog.sh
</pre>


# Common reasons for disk utilization on Confluence/JIRA exceeding 75%
1) /var/atlassian/application-data/confluence/backups  (local backups enabled - default behavior unless manually disabled)
2) /opt/atlassian/confluence/logs/catalina.out         (file not rotated regularly)
 
# How to resize/extend Linux File System after resizing the root volume on an EC2 Ubuntu instance
From the EC2 management console, select EBS volume and resize volume
Once the state updates to "in use - optimizing' ssh to EC2 instance to expand the mounted filesystem
<p>
<pre>
Use Case 1 - XFS File System
'$ lsblk' to get filesystem name
'$ sudo growpart /dev/nvme0n1 1' where 1 designates the partition you want to grow and nvme0n1 is the filesystem 
'$ lsblk' to confirm partition reflects new size
'$ sudo yum install xfsprogs' to install XFS tools if not already installed
'$ sudo xfs_growfs -d /dev/nvme0n1p1' to resize filessystem where /dev/nvme0n1p1 designates the mount point from df -h
'$ df -h' to verify filesystem was successfully resized

<p>

Use Case 2 - ext2, ext3, or ext4 File System
'$ lsblk' to get filesystem name
'$ sudo growpart /dev/xvda 1' where the space designates the partition you want to grow 
'$ lsblk' to confirm partition reflects new size
'$ sudo resize2fs /dev/xvda1' to resize filessystem
'$ df -h' to verify filesystem was successfully resized

<p>  

(Source: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html)
Extending a Linux File System After Resizing a Volume https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html
</pre>

# Creating IAM Group and policy to allow IAM users to view the AWS Cost Explorer dashboard
<pre>
Create new IAM group named CostExplorerReadOnlyGroup with attached policy named CostExplorerReadOnlyPermissions:

CostExplorerReadOnlyPermissions IAM Policy
{
   "Version": "2012-10-17",
   "Statement": [
       {
           "Sid": "VisualEditor0",
           "Effect": "Allow",
           "Action": "cur:DescribeReportDefinitions",
           "Resource": "*"
       },
       {
           "Effect": "Allow",
           "Action": [
               "aws-portal:*Billing",
               "aws-portal:*Usage",
               "aws-portal:*PaymentMethods"
           ],
           "Resource": "*"
       },
       {
           "Effect": "Deny",
           "Action": "aws-portal:*Account",
           "Resource": "*"
       }
   ]
}
</pre>

# CloudZero X-ray SDK 

1) Create your Lambda

2) Export your Lambda as zip file

3) Install the CloudZero X-ray SDK in a virtualenv using pip

4) Install dependency modules local to the function project (ie: boto3)
<pre>
   $ pip install boto3 -t ./   (-t installs packages into <dir>. By default this will not replace existing files/folders in <dir>.)
   $ pip install aws-xray-sdk -t ./
   $ pip install tox -t ./
</pre>

5) Insert CloudZero X-ray SDK import and api statements
<pre>
Example:
# For Xray Tracing
# Place at top of Lambda handlers
import botocore  # noqa
from aws_xray_sdk.core import xray_recorder
from aws_xray_sdk.core import patch_all
xray_recorder.configure(context_missing='LOG_ERROR')
patch_all()
</pre>

6) Manually build a Lambda deployment package and create zip file in parent directory of project
<pre>
zip -r ../myDeploymentPackage.zip   (-r recurses into directories)
</pre>

7) Verify deployment package
<pre>
$ cd ..
$ unzip -l myDeploymentPackage.zip  (-l lists files in short format)
</pre>

8) Create new Lambda, upload deployement package and provision any addtional Lambda specific settings
   (For example, IAM  policies/role, Lambda execution time, event trigger, etc.) and remember to 
   enable active tracing!) 
<pre>
If you get an error "No module named lambda_function",
rename the default Lambda function handler so it uses Python_File_Name.Method_Name from the Lambda management console.
For example: 
Python filename: cloudzero_xray_sdk_lambda.py

Lambda handler field should be: cloudzero_xray_sdk_lambda.lambda_handler
</pre>

9) Test your Lambda


Resources: <br>
[CloudZero X-ray SDK Repo](https://github.com/Cloudzero/aws-xray-sdk-python) <br>
[How do I build an AWS Lambda deployment package for Python?](https://aws.amazon.com/premiumsupport/knowledge-center/build-python-lambda-deployment-package/) <br>

# How to version control your Lambdas
Write a script to deploy the lambda given the location of a zip file that resides in a version control system.

Then deploy the Lambda from the repo.

Steps the script should take:
1. git clone the repo
2. run the requirement.txt or whatever to get the correct libraries
3. zip up everything
4. Push to AWS Lambda

*Putting software hat on* This process should be encapsulated within a build process (ie: Jenkins) and the code should have to pass some reasonable tests.

# How to quickly query RDS MySQL database using mysql run from EC2

## Connecting to RDS database
mysql -h <rds-endpoint> -P <port> -u <rds_username> -p

## Useful mysql commands
<pre>
show databases;
use database_name;
show tables;
describe table_name;
</pre>

Example for (Confluence issue)[https://jira.atlassian.com/browse/CONFSERVER-55274?utm_source=STP&utm_medium=logScan]:
select count(bandanaid) from BANDANA where BANDANAKEY like '%com.atlassian.oauth.serviceprovider.ServiceProviderTokenStore.token%';

Note: 
1) mysql doesn't like spaces after function names which is why `count(bandanaid)` and not `count (bandanaid)` is used
2) mysql database names are case sensitive which is why `BANDANA` and not `bandana` is used

<pre>
select * FROM table_name;
select * FROM field_name;
</pre>

Resource: (MySQL 101)[https://www.globo.tech/learning-center/mysql-101-basics/]

# Modifying a list of objects curated from an S3 Batch Operations completion report
<pre>
The objects listed in an S3 Batch Operations completion report are not surrounded with quotation marks and contain alot of "garbage" information.
You can use VIM to strip each row down to just the S3 keys. (eg: :%s/,,.*// , delete everything from ,, to end of line)
After doing that locally, import the result file to GoogleSheets and add columns containing quotations on each side.
Download the GoogleSheet as a csv file.
Use VIM to replace the """", and ,"""" marks with single quotes.
Use the final artifact that can be read in as a list in Python.

If you exceed GoogleSheet's maximum supported cells, then use VIM and do the following:
1) Go to record mode: Type 'q' followed by any letter [a-z]. Enter insert mode and add quotation in beginning of first line,
add quotation to end of line, add comma to end of line, then move to beginning of next line
2) Type 'q' to stop the recording
3) Type N@[a-z] where N is number of iterations you'd like to repeat the recording and [a-z] is the letter you used in step 1. Tip: You can get N by jumping to the bottom of the file then use (N-1) as the number of iterations to use.
5) Remember to remove the comma at the end of the last line and to clean up any funny looking filenames that may contain spaces.
You'll know by searching for '++++' (plus signs)
</pre>

# How to Prompt for User Input in Linux Shell Script
(link)[https://tecadmin.net/prompt-user-input-in-linux-shell-script/]

# How to search multiple words/string pattern using grep command on Bash shell
<pre>
Simple example: 
aws cloudtrail lookup-events --lookup-attributes AttributeKey=ResourceName,AttributeValue=not-real-bucket  | grep 'EventName\|Username'


The syntax is:
Use single quotes in the pattern: grep 'pattern*' file1 file2
Use extended regular expressions: egrep 'pattern1|pattern2' *.py
Use this syntax on older Unix shells: grep -e pattern1 -e pattern2 *.pl

Here are all other possibilities:
grep 'word1\|word2\|word3' /path/to/file
### Search all text files ###
grep 'word*' *.txt
### Search all python files for 'wordA' or 'wordB' ###
grep 'wordA*'\''wordB' *.py
grep -E 'word1|word2' *.doc
grep -e string1 -e string2 *.pl
egrep "word1|word2" *.c
</pre>

# How to take user input in Bash shell
<pre>
# User input
read -p "Enter AWS username: " aws_username
read -p "Enter GHE username: " ghe_username
read -s -p "Enter GHE password: " ghe_password

echo $aws_username
echo $ghe_username
echo $ghe_password
</pre>

# How to invoke boto3 script using a non-default AWS profile
<pre>
""" Example using default profile """
client = boto3.client('s3')
print client.put_object_acl(Bucket=bucketname,Key=i,ACL='bucket-owner-full-control',)

""" Example using non-default profile """
foo  = boto3.session.Session(profile_name='foo')
foo_client = miru.client('s3')
print foo_client.put_object_acl(Bucket=bucketname,Key=i,ACL='bucket-owner-full-control',)
</pre>
[StackOverflow](https://stackoverflow.com/questions/33378422/how-to-choose-an-aws-profile-when-using-boto3-to-connect-to-cloudfront)

# How to create a bot user to access GitHub Enterprise repositories
First, verify your admin-capable GHE user has 'site-admin' permissions. 
<p>
<p>
Login to GHE, select 'Settings' from the profile icon located in the upper right corner, click 'Developer settings', click 'Personal access tokens', click on token, then verify 'site-admin' checkbox is selected.
<p>

## API Example
<pre>
curl -u "david-lin:\&lttoken&gt" -X POST -d @&ltbot-user-name-goes-here&gt-bot.json &ltURL&gt/api/v3/admin/users --header "Content-Type:application/json" 

where:
   - david-lin is the admin-capable GHE user and &lttoken&gt is then user's token (not shown)
   - &ltbot-user-name-goes-here&gt-bot.json is a plain text json file (see below)
   - URL is the API endpoint on the GHE server ( for example, https://github.awsinternal.domain.name )
</pre>

### Example JSON file
<pre>
{"login": "david-lin-bot-user"} 
</pre>

# Generating MD5 Checksum
Windows 10
<pre>
Using MS File Checksum Integrity Verifier
1. Copy file to a folder on your Desktop (e.g. \Desktop\foo)
2. Open Powershell and navigate to the folder (e.g. cd .\Desktop\foo)
3. Type `./fciv -md5 &ltfilename&gt`

Using PowerShell
1. Get-FileHash -Algorithm MD5
2. Path[0] Example:  C:\Users\David\Desktop\filename.txt
3. Path[1]: leave blank
</pre>

# Crontab
<pre>
$ crontab -l   lists cron jobs
$ crontab -e   editor mode

Note: POSIX requires a trailing newline character to consider any line to be complete
</pre>
[Simple Cron Editor](https://crontab.guru/)
<br>
[AWS Schedule Expressions](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html)
<br>
[Cron examples](https://github.com/davidclin/cloudcustodian-policies#running-policy-as-cron-job)
<br>
[Cron requires a newline character on its own line at the end of the file](https://superuser.com/questions/1059775/cron-apparently-requires-a-newline-character-on-its-own-line-at-the-end-of-the-f)

# AWS Elastic Container Registry (ECR) IAM permission policy example
The following policy is applied under the ECR repository permissions settings.
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "MlSandboxAccess",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123456789012:root"
      },
      "Action": [
        "ecr:BatchCheckLayerAvailability",
        "ecr:BatchGetImage",
        "ecr:DescribeImageScanFindings",
        "ecr:DescribeImages",
        "ecr:DescribeRepositories",
        "ecr:GetAuthorizationToken",
        "ecr:GetDownloadUrlForLayer",
        "ecr:ListImages",
        "ecr:ListTagsForResource"
      ]
    }
  ]
}

Note: Users also require IAM permissions to perform the action ecr:GetAuthorizationToken to perform pull/push requests.
</pre>

# S3 Bucket Policy Examples
https://docs.aws.amazon.com/AmazonS3/latest/dev/example-bucket-policies.html#example-bucket-policies-use-case-8

# S3 Public Bucket Policy Use Cases
Basic public read access
 <pre>
 {
    "Version": "2008-10-17",
    "Statement": [
        {
            "Sid": "AllowPublicRead",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::<bucket-name>/*"
        }
    ]
}
</pre>

Basic Read/Write Access with IAM user allow list
<pre>
{
    "Id": "Policy1572303525647",
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "IAMUserWhiteList",
            "Action": "s3:*",
            "Effect": "Deny",
            "Resource": "arn:aws:s3:::BUCKETNAME",
            "NotPrincipal": {
                "AWS": [
                    "arn:aws:iam::929292782238:user/david.lin",
                    "arn:aws:iam::929292782238:user/rick.hunter",
                    "arn:aws:iam::929292782238:user/lisa.hayes",
                    "arn:aws:iam::929292782238:user/roy.foker"
                ]
            }
        }
    ]
}
</pre>

Basic Get* and List* Actions
<pre>
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:Get*",
                "s3:List*"
            ],
            "Resource": [
                "arn:aws:s3:::bucket-name-goes-here",
                "arn:aws:s3:::bucket-name-goes-here/*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": ["s3:ListAllMyBuckets","s3:HeadBucket"],
            "Resource": "*"
        }
    ]
}
</pre>

Basic ListAllMyBuckets, GetObject and PutObject
<pre>
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:ListAllMyBuckets",
                "s3:HeadBucket"
            ],
            "Resource": "*"
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "s3:GetObject*",
                "s3:PutObject*"
            ],
            "Resource": [
                "arn:aws:s3:::bucket-name-goes-here",
                "arn:aws:s3:::bucket-name-goes-here/*"
            ]
        }
    ]
}
</pre>

If you plan on using aws s3 sync, use the following at a minimum:
<pre>
{
    "Version": "2008-10-17",
    "Statement": [
        {
            "Sid": "AllowPublicRead",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": "s3:GetObject",
            "Resource": [
                "arn:aws:s3:::XXX/*",
                "arn:aws:s3:::XXX"
            ]
        },
        {
            "Sid": "AllowPublicRead",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": "s3:ListBucket",
            "Resource": [
                "arn:aws:s3:::XXX/*",
                "arn:aws:s3:::XXX"
            ]
        }
    ]
}
</pre>

Permit based on IpAddress and HTTPS
<pre>
{
    "Version": "2008-10-17",
    "Id": "S3Policy",
    "Statement": [
        {
            "Sid": "IPDeny",
            "Effect": "Deny",
            "Principal": {
                "AWS": "*"
            },
            "Action": "s3:*",
            "Resource": "arn:aws:s3:::tri-ses-dashboard/*",
            "Condition": {
                "NotIpAddress": {
                    "aws:SourceIp": [
                        "x.x.x.x",
                        "x.x.x.x",
                        "x.x.x.x"
                    ]
                }
            }
        },
        {
            "Sid": "HTTPDeny",
            "Effect": "Deny",
            "Principal": {
                "AWS": "*"
            },
            "Action": "s3:*",
            "Resource": "arn:aws:s3:::tri-ses-dashboard/*",
            "Condition": {
                "Bool": {
                    "aws:SecureTransport": "false"
                }
            }
        }
    ]
}
</pre>

Permit public access if bucket has public website hosting enbled but only allow access based on IP address 
<pre>
{
    "Version": "2008-10-17",
    "Statement": [
        {
            "Sid": "AllowPublicRead",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::bucketname/*"
        },
        {
            "Sid": "IPDeny",
            "Effect": "Deny",
            "Principal": {
                "AWS": "*"
            },
            "Action": "s3:*",
            "Resource": "arn:aws:s3:::bucketname/*",
            "Condition": {
                "NotIpAddress": {
                    "aws:SourceIp": [
                        "x.x.x.x",
                        "x.x.x.x",
                        "x.x.x.x"
                    ]
                }
            }
        }
    ]
}
</pre>

Permit IAM User(s) only
<pre>
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "WhitelistExampleBucket",
            "Effect": "Deny",
            "NotPrincipal": {
                "AWS": [
                    "arn:aws:iam::929292782238:user/david.lin"
                ]
            },
            "Action": "s3:*",
            "Resource": "arn:aws:s3:::bucketname/*"
        }
    ]
}
</pre>

Permit accounts and require the bucket-owner-full-control condition for PutObject operations
<pre>
{
    "Version": "2012-10-17",
    "Id": "Policy1530302529355",
    "Statement": [
        {
            "Sid": "Stmt1530302524307",
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::111111111111:root",
                    "arn:aws:iam::222222222222:root"
                ]
            },
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::example-bucket/*",
                "arn:aws:s3:::example-bucket"
            ]
        },
        {
            "Sid": "RefuseAllPutsFromOtherAccountsWithoutFullControlACL",
            "Effect": "Deny",
            "Principal": {
                "AWS": "*"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::example-bucket/*",
            "Condition": {
                "StringNotEquals": {
                    "s3:x-amz-acl": "bucket-owner-full-control"
                }
            }
        },
        {
            "Sid": "Account Access",
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::111111111111:root",
                    "arn:aws:iam::333333333333:root",
                    "arn:aws:iam::444444444444:root",
                    "arn:aws:iam::222222222222:root"
                ]
            },
            "Action": [
                "s3:Get*",
                "s3:Put*",
                "s3:List*"
            ],
            "Resource": [
                "arn:aws:s3:::example-bucket/*",
                "arn:aws:s3:::example-bucket"
            ]
        },
        {
            "Sid": "Account Read-only Access",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::555555555555:root"
            },
            "Action": [
                "s3:Get*",
                "s3:List*"
            ],
            "Resource": [
                "arn:aws:s3:::example-bucket/*",
                "arn:aws:s3:::example-bucket"
            ]
        }
    ]
}

</pre>

Whitelist IAM users allowed to read/write to bucket resource. When attached to an IAM Group that has the AmazonS3FullAccess policy attached, it will allow all users in the IAM Group to read but only IAM users in the whitelist to write to the S3 buckets defined.
<pre>
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowS3ReadAccess",
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::example-bucket",
                "arn:aws:s3:::example-bucket/*"
            ]
        },
        {
            "Sid": "AllowS3HeadObjectAccess",
            "Effect": "Allow",
            "Action": "s3:HeadObject",
            "Resource": [
                "arn:aws:s3:::example-bucket",
                "arn:aws:s3:::example-bucket/*"
            ]
        },
        {
            "Sid": "DenyS3WriteAccessExceptWhitelist",
            "Effect": "Deny",
            "Action": [
                "s3:PutObject",
                "s3:DeleteObjectVersion",
                "s3:PutObjectVersionAcl",
                "s3:DeleteObject",
                "s3:PutObjectAcl"
            ],
            "Resource": [
                "arn:aws:s3:::example-bucket",
                "arn:aws:s3:::example-bucket/*"
            ],
            "Condition": {
                "StringNotEquals": {
                    "aws:PrincipalArn": [
                        "arn:aws:iam::929292782238:user/david.lin",
                        "arn:aws:iam::929292782238:user/john.doe"                        
                    ]
                }
            }
        }
    ]
}
</pre>

# S3 Copy Objects from Source Account to Destination Account
The following example demonstrates how you can copy objects from a source account to a destination account while granting bucket-owner-full-control.

Step 1) Attach the following bucket policy to the destination bucket
<pre>
{
    "Version": "2012-10-17",
    "Id": "Policy1563469398098",
    "Statement": [
        {
            "Sid": "Stmt1563469394390",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::929292782238:user/AWS_IAM_USER_NAME"
            },
            "Action": "s3:*",
            "Resource": "arn:aws:s3:::TARGET_BUCKET_NAME/*"
        }
    ]
}
</pre>

Step 2) Issue the following AWS CLI using the Principal that was specified in the bucket policy
<pre>
$ aws s3 cp s3://SOURCE_BUCKET/ s3://DESTINATION_BUCKET/ --acl bucket-owner-full-control --recursive
</pre>

# S3 Cross Account Permissions and Deny Puts without bucket-owner-full-control
<pre>
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowPutObject",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::{crossaccount}:root"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::annotations-staging/sagemaker/*"
        },
        {
            "Sid": "DenyIfBucketOwnerFullControlIsNotSet",
            "Effect": "Deny",
            "Principal": {
                "AWS": "arn:aws:iam::{crossaccount}:root"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::annotations-staging/sagemaker/*",
            "Condition": {
                "StringNotEquals": {
                    "s3:x-amz-acl": "bucket-owner-full-control"
                }
            }
        },
        {
            "Sid": "AllowListBucket",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::{crossaccount}:root"
            },
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::annotations-staging"
        },
        {
            "Sid": "AllowGet",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::{crossaccount}:root"
            },
            "Action": "s3:Get*",
            "Resource": "arn:aws:s3:::annotations-staging/sagemaker/*"
        },
        {
            "Sid": "S3BucketToBucket",
            "Effect": "Allow",
            "Principal": {
                "Service": "s3.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::annotations-staging/*",
            "Condition": {
                "StringEquals": {
                    "s3:x-amz-acl": "bucket-owner-full-control",
                    "aws:SourceAccount": "{sourceaccount}"
                },
                "ArnLike": {
                    "aws:SourceArn": "arn:aws:s3:::scratch-tri-global"
                }
            }
        }
    ]
}
</pre>

# S3 Update ACL for all objects in folder with bucket-owner-full-control
<pre>
aws s3 cp s3://bucketname/folder1/ s3://bucketname/folder1/ --recursive --acl bucket-owner-full-control --metadata updated=$(date)
</pre>

# How to make a Google Cloud bucket public
<pre>
gsutil acl ch -u AllUsers:R gs://[your-storage-bucket]/cdn.png
</pre>

# How to connect to a Google Cloud compute engine that only has an internal IP address from a bastion host
<pre>
gcloud compute ssh [vm-name] --zone=us-central1-a --internal-ip
</pre>

# How to quickly launch multiple Google Cloud compute engines using the CLI from Cloud Shell
<pre>
// Launch 3 compute engines
for i in {1..3}; \
do \
  gcloud compute instances create "nginxstack-$i" \
  --machine-type "f1-micro" \
  --tags nginxstack-tcp-443,nginxstack-tcp-80 \
  --zone us-central1-f \
  --image   "https://www.googleapis.com/compute/v1/projects/bitnami-launchpad/global/images/bitnami-nginx-1-16-0-0-r50-linux-debian-9-x86-64" \
  --boot-disk-size "200" --boot-disk-type "pd-standard" \
  --boot-disk-device-name "nginxstack-$i"; \
done

// Create tagged firewall rules for newly created compute engines
gcloud compute firewall-rules create nginx-firewall \
 --allow tcp:80,tcp:443 \
 --target-tags nginxstack-tcp-80,nginxstack-tcp-443

</pre>
