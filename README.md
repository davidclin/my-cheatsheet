# Cheatsheet
David's Cheatsheet and Examples

# Good practice whenever you update Ubuntu on an EC2 instance
<pre>
$ df  (check available disk space)

$ cd /usr/src
$ ll  (check for stale packages)

$ sudo apt update && sudo apt full-upgrade
$ sudo apt autoremove

$ df (check reclaimed disk space)
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

Some good places to start are:
1) /var directory (if this is a Confluence/JIRA server)
2) /usr/source (if this is an ec2 instance, look for stale linux-aws-headers-x.x.x-xxxx binaries then issue `sudo apt update && sudo apt full-upgrade` followed by `sudo apt autoremove` to clean them out) 

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
1. Copy file to a folder on your Desktop (e.g. \Desktop\foo)
2. Open Powershell and navigate to the folder (e.g. cd .\Desktop\foo)
3. Type `./fciv -md5 &ltfilename&gt` 
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
            "Action": "s3:ListAllMyBuckets",
            "Resource": "*"
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
