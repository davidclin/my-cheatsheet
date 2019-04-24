# Cheatsheet
David's Cheatsheet and Examples

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

# S3 CLI Tuning
AWS CLI S3 performance improves if you tune it. Modify your ~/.aws/config to file to contain the following (place it under [default] and any additional profiles you use with S3):

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
</pre>

Resource: https://docs.python-guide.org/dev/virtualenvs/

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

# How to find large files
<pre>
See disk utilization
$ df

Start from root directory and issue:
$ sudo du -sh *

Another good place to start is the /var directory (if this is a Confluence/JIRA server)

Change into suspect directory and repeat command until you find source of large files.
</pre>

# How to truncate large log file
<pre>
# Make sure to backup file 
$ aws s3 cp filename.txt s3://bucketname

#Trunkcate file
$ truncate -s 0 myfile.txt
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
Issue 
'$ lsblk' to get filesystem name
'$ sudo growpart /dev/xvdf 1' where the space designates the partition you want to grow 
'$ lsblk' to confirm partition reflects new size
'$ sudo resize2fs /dev/xvda1' to resize filessystem
'$ df -h' to verify filesystem was successfully resized
<p>  
(Source: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html)
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
You can use VIM to strip each row down to just the S3 keys.
After doing that, copy the result to GoogleSheets and add columns containing quotations on each side.
Download the GoogleSheet as a csv file.
Use VIM to replace the """", and ,"""" marks with single quotes.
Use the final artifact that can be read in as a list in Python.
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
