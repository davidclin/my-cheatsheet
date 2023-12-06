![Banner](https://github.com/davidclin/cheatsheet/blob/master/images/banner.png)
  

# Beautify your terminal to make it more enjoyable
![Image of Terminal](https://github.com/davidclin/cheatsheet/blob/master/images/cowsay.GIF)
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

# How to create animated screen captures in GIF
<pre>
LICEcap - https://www.cockos.com/licecap/
</pre>

# How to create Chrome group tabs
<pre>
1) Go to chrome://flags and then use the search bar to find the “tab-groups-save” option.
2) Alongside the option you’ll see a drop down menu to enable or disable to feature. 
3) Enable it to use it. 
4) After that, click “Relaunch” which will save the flag changes and restart the browser. 
5) After that the Tab Groups Save option should be enabled when you right-click on the tab group name.
6) Saved groups will appear on the bookmarks panel.
7) At this point, you can just open new a chrome window, click on group name on the bookmark panel and the group opens in new window.
</pre>

# How to use osquery (interactive mode)
<pre>
============================
Install via apt-get (Debian)
============================
export OSQUERY_KEY=1484120AC4E9F8A1A577AEEE97A80C63C9D8B80B
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys $OSQUERY_KEY
sudo add-apt-repository 'deb [arch=amd64] https://pkg.osquery.io/deb deb main'
sudo apt-get update
sudo apt-get install osquery

======
Verify
======
osqueryi --version

===========================
Using the Interactive Shell
===========================
osqueryi
.help
.quit
.tables
.schema <table_name>
.mode [line, pretty, csv, column, list]  <----- Super useful

Example query from uptime table (don't forget the ; at the end)
select days, hours, minutes from uptime;

More examples:
select * from uptime;   OR  .all uptime

The rest is all up to you and your ninja SQL skills. Have fun!

=========
Resources
=========
https://www.cloudsavvyit.com/9184/use-sql-and-osquery-to-interrogate-your-hardware-on-linux/
https://osquery.readthedocs.io/en/stable/
</pre>

# How to quickly get date and time on Ubuntu from terminal
<pre>
date "+%H:%M:%S   %d/%m/%y"        
</pre>
        
# How to open multiple AWS management consoles for different accounts using Okta with AWS SSO and Firefox browser
<pre>
General procedure
1. Install the Firefox Containers plugin extension here https://addons.mozilla.org/en-US/firefox/addon/multi-account-containers/
2. Use 1 window per FF container per account ( example 10 windows = 10 different accounts )
3. Open a FF window inside container and login using OKTA -> AWS SSO page and pick the account and open multiple tabs for each service you will be working in
4. Repeat step 3 for subsequent accounts
5. Store the container with the name of account + number for future use

PowerUser
1. Install tree-style-tabs https://addons.mozilla.org/en-US/firefox/addon/tree-style-tab/
</pre>

# The Heilmeier Catechism
The Heilmeier Catechism is a set of questions designed to get to the core of a project idea. It was developed by George H. Heilmeier at DARPA.<br>
<p>
New proposals should aim to answer the following questions:<br>
<p>
What are you trying to do? Articulate your objectives using absolutely no jargon.<br>
How is it done today, and what are the limits of current practice?<br>
What is new in your approach and why do you think it will be successful?<br>
Who cares? If you are successful, what difference will it make?<br>
What are the risks?<br>
How much will it cost?<br>
How long will it take?<br>
What are the mid-term and final "exams" to check for success?<br>

# Expandable Markdown
![Code example](https://github.com/davidclin/cheatsheet/blob/master/images/expandable_markdown.gif)
<details>
<summary>Click here to see example in action</summary>

<pre>
That was easy!
</pre>
</details>

# Markdown
<pre>
--- Images ---
![optional-description-goes-here](url-goes-here)

--- Links ---
(url-goes-here)
[TextGoesHere](url-goes-here)

--- Headers ---
| #  This is an h1 tag
| ## This is an h2 tag

--- Fonts ---
| *This text will be italic*
| _This text will also be italic_
| **This text will be bold**
| __This text will also be bold__

--- Lists ---
Unordered
| * Item 1
| * Item 2
|   * Item 2a
|   * Item 2b

Ordered
| 1. Item 1
| 1. Item 2
| 1. Item 3
|   1. Item 3a
|   1. Item 3b

--- Blockquotes ---
As I once said,
> In a galaxy far, far, away...
</pre>

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

# How to ssh using ~/.ssh/config file
<pre>
Place following in ~/.ssh/config

Host EXAMPLE-NAME-GOES-HERE
  HostName fully-qualified-domain-name OR ip-address-of-host
  User ubuntu (or username)
  Port 22 (or custom port)
  IdentityFile ~/.ssh/foo.pem  (private ssh key)
  
Then, ssh EXAMPLE-NAME-GOES-HERE

Above is equivalent to ssh -p Port -i IdentityFile User@HostName
</pre>

# SSH Troubleshooting Tips
<pre>
https://phoenixnap.com/kb/ssh-permission-denied-publickey
https://docs.github.com/en/github/authenticating-to-github/troubleshooting-ssh/error-permission-denied-publickey
https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

Another common issue can occur when copying/pasting pub key to ~/.ssh/authorized_keys.
Make sure it's a continuous string and there are no hidden carriage returns!        
</pre>
        
# How to use git so it doesn't ask for username/password everytime
![Image of SSH Keys](https://github.com/davidclin/cheatsheet/blob/master/images/ghe-ssh-keys.gif)
<pre>
Generate an SSH key pair and add it to your SSH credentials under your GitHub user profile.
Then clone the repository using the SSH string; not the HTTPS URL.

Example: git clone git@github.awesomesauce.com:MySandbox/cloudcustodian.git
</pre>

# How to get the Canonical ID of an AWS account
<pre>
https://docs.aws.amazon.com/general/latest/gr/acct-identifiers.html
</pre>

# How to get list of AWS accounts in an Organization
<pre>
aws organizations list-accounts
</pre>

# How to get secret from AWS Secrets Manager
<pre>
From local account
aws secretsmanager get-secret-value --secret-id KEY_NAME_GOES_HERE

From cross account using an IAM role 
aws secretsmanager get-secret-value --secret-id KEY_NAME_GOES_HERE --version-stage AWSCURRENT --profile IAM_PROFILE_GOES_HERE
</pre>

# AWS CloudWatch Agent
How to see status
```
systemctl status amazon-cloudwatch-agent.service
```
Example output:
<pre>
mazon-cloudwatch-agent.service - Amazon CloudWatch Agent
   Loaded: loaded (/etc/systemd/system/amazon-cloudwatch-agent.service; enabled; vendor preset: disabled)
   Active: active (running) since Fri 2023-06-09 06:19:10 UTC; 4 months 9 days ago
 Main PID: 2116 (amazon-cloudwat)
    Tasks: 11
   Memory: 26.2M
   CGroup: /system.slice/amazon-cloudwatch-agent.service
           └─2116 /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent -config /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.toml -envconfig /opt/aws/amazon-cloudwatch-agent/etc/env-config.json -pidfile /opt/aws/amazon-cloudwat...
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

# How to determine which Availability Zones a particular instance type is supported in | Keyword: ICE 
<pre>
Example for p3dn.24xlarge:
aws ec2 describe-instance-type-offerings --location-type availability-zone --filters Name=instance-type,Values=p3dn.24xlarge --region us-east-1

</pre>

# How to quickly determine the IAM role attached to a Jenkins worker if you don't have access to the Jenkins master
<pre>
$ curl http://169.254.169.254/latest/meta-data/iam/info ; echo
{
  "Code" : "Success",
  "LastUpdated" : "2020-03-10T22:37:58Z",
  "InstanceProfileArn" : "arn:aws:iam::123456789012:instance-profile/jenkins-slave-1",
  "InstanceProfileId" : "AIPAJSDGYFQQZD5F22RI3"
}
</pre>

# How to update AWS username using AWS CLI
<pre>
aws iam update-user --user-name Bob --new-user-name Robert
</pre>

# How to quickly determine the identity of an AWS IAM user or role using the AWS CLI in addition to getting the Canonical ID of account
<pre>
$ aws sts get-caller-identity

{
    "Account": "123456789012",
    "UserId": "AIDRTESY24R55OHEHXXXX",  <----------- userId
    "Arn": "arn:aws:iam::123456789012:user/david"
}

$ aws iam get-user --user-name david.lin

{
    "User": {
        "UserName": "david.lin",
        "PasswordLastUsed": "2020-10-07T17:25:56Z",
        "CreateDate": "2018-02-23T00:26:45Z",
        "UserId": "AIDAIZSY24R55OHEHXXXX",
        "Path": "/",
        "Arn": "arn:aws:iam::929292782238:user/david.lin"
    }
}

$ aws iam get-role --role-name ROLE-NAME

{
    "Role": {
        "Path": "/",
        "RoleName": "test_role",
        "RoleId": "AROAWFF63FQHG3NHXXXXX",  <------------------ roleId
        "Arn": "arn:aws:iam::111111111111:role/test-role",
        "CreateDate": "2020-08-17T16:19:37Z",
        (snip)
}  

$ aws s3api list-buckets --query Owner.ID --output text  [--profile xxx]
Note: Permission to allow s3:ListBucket against resource * may be needed

</pre>

# How to set AWS environment variables
<pre>
export AWS_ACCESS_KEY_ID=xxx
export AWS_SECRET_ACCESS_KEY=xxx
export AWS_DEFAULT_REGION=xxx

Verify with:
aws sts get-caller-identity
</pre>
# How to assume IAM role using AWS CLI
<pre>
unset AWS_ACCESS_KEY_ID AWS_SECRET_ACCESS_KEY AWS_SESSION_TOKEN

aws sts assume-role --role-arn "arn:aws:iam::111111111111:role/my-iam-role-name" --role-session-name foo

export AWS_ACCESS_KEY_ID=xxx
export AWS_SECRET_ACCESS_KEY=xxx
export AWS_SESSION_TOKEN=xxx

aws sts get-caller-identity

Remember: The IAM role requires a trust policy that permits principal to assume the role. 

Source: https://aws.amazon.com/premiumsupport/knowledge-center/iam-assume-role-cli/
</pre>

# How to determine owner of an S3 object
<pre>
aws s3api get-object-acl --bucket BUCKETNAME --key SomeS3Prefix/random_file_v001.json
{
    "Owner": {
        "DisplayName": "david",
        "ID": "a7ca22384dc4054b0d52f0e6279b381deff8e1d26f062b0be99386XXXXXXXXXX"
    }
</pre>

# How to troubleshoot S3 bucket owner full control issues
<pre>
Cryptic error: fatal error: An error occurred (403) when calling the HeadObject operation: Forbidden

Lesson Learned:

o Use the --debug option (AWS support can use the IDs to dig into logs on the backend)

o To get the Canonical ID of bucket owner account
  aws s3api list-buckets --query Owner.ID --output text  [--profile xxx]
  
  The Canonical ID is used when an object(s) needs to be shared with another account

o To share an object that was copied with --acl bucket-owner-full-control from the bucket account with a 3rd account,
  you can use the management console or CLI like so:

  aws s3api put-object-acl --bucket permissionstest123456 --key testing --grant-full-control id="0d63e3b3b8fa5842b881b799cf2ff71c78a725fc461ead2ab03a26a22bfbd638"

o Cloudtrail, CloudWatch, and Bucket access logging are your friends
</pre>

# How to quickly view an ec2 instance's user data 
<pre>
$ curl http://169.254.169.254/latest/user-data
</pre>

# How to grab detailed metadata of your EC2 instance
<pre>
curl http://169.254.169.254/latest/meta-data/                                                           get list of available objects
curl http://169.254.169.254/latest/meta-data/identity-credentials/ec2/info/                             get AccountId
curl http://169.254.169.254/latest/meta-data/network/interfaces/macs/<mac-address>/owner-id/            get AccountId
curl http://169.254.169.254/latest/meta-data/placement/region/                                          get region
curl http://169.254.169.254/latest/meta-data/placement/availability-zone/                               get availability zone
curl http://169.254.169.254/latest/meta-data/instance-id/                                               get instance-id
curl http://169.254.169.254/latest/meta-data/local-ipv4/                                                get ipv4 address
curl http://169.254.169.254/latest/meta-data/network/interfaces/macs/<mac-address>/subnet-id/           get subnet-id
curl http://169.254.169.254/latest/meta-data/network/interfaces/macs/<mac-address>/vpc-id/              get vpc-id
curl http://169.254.169.254/latest/meta-data/instance-type/                                             get instance type
curl http://169.254.169.254/latest/meta-data/security-groups                                            get security-groups
curl http://169.254.169.254/latest/meta-data/iam/info/                                                  get instance profile arn + id
curl http://169.254.169.254/latest/meta-data/hostname                                                   get hostname 
curl http://169.254.169.254/latest/meta-data/public-keys                                                get ssh key name
curl http://169.254.169.254/latest/user-data                                                            get user-data    
curl http://169.254.169.254/latest/meta-data/ami-id                                                     get ami-id
curl http://169.254.169.254/latest/meta-data/local-hostname                                             get local hostname

curl http://169.254.169.254/latest/meta-data/public-keys/0/openssh-key                                  get public key
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

How to loop through list and export to file:
<pre>
USER=David,Trevor,Brooke
echo '----'
echo 'Stuff'
echo '----'

for i in $(echo $USER | sed "s/,/ /g")
do
  \# Loop through the USER list
  echo $i
  echo <shell_cmd> >> results.txt
done
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

# Reset your AWS access key environment variables
```
export AWS_ACCESS_KEY_ID=""
export AWS_SECRET_ACCESS_KEY=""
export AWS_SESSION_TOKEN=""
```

# AWS EC2 Resources
[EC2Instances.info](https://ec2instances.info/?min_memory=8&min_vcpus=4&min_storage=20&selected=m5a.2xlarge,i3en.12xlarge,i3en.metal,t2.micro)
<br>
[Amazon EC2 AMI Locator (Ubuntu)](https://cloud-images.ubuntu.com/locator/ec2/)

# AWS IAM References
[Complete AWS IAM Reference](https://iam.cloudonaut.io/)

# How to run Docker as a non-root user
<pre>
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
$ newgrp docker
$ docker run hello-world

For more info: https://docs.docker.com/engine/install/linux-postinstall/
</pre>

# How to create an alias in Linux
From your user's home path (just type `cd` + enter), add the following line to .bashrc
<pre>
alias="command-goes-here"
</pre>
Don't forget to exit your shell and login back in for the alias to take effect.

# How to connect to MySQL in Linux
<pre>
$ sudo apt install mysql-client-core-5.7
$ mysql -u $USERNAME -h $HOSTNAME -P $PORT_NUMBER -p 
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

To get output beautified add the following lines

$ aws sts decode-authorization-message --encoded-message {copy/paste encoded msg here} |
        jq '.["DecodedMessage"]' |
        sed 's/\\"/"/g' |
        sed 's/^"//' |
        sed 's/"$//' |
        jq
        
Note: This requires jq.
More info: https://thoughtbot.com/blog/jq-is-sed-for-json
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
unset AWS_SESSION_TOKEN

or simply... 

unset AWS_SECRET_ACCESS_KEY AWS_ACCESS_KEY_ID AWS_SESSION_TOKEN

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
$ virtualenv env -p 
(alternative)
</pre>

Resource: https://docs.python-guide.org/dev/virtualenvs/

# How to install and start/deactivate a Python3 virtual environment (with AWS CLI and Boto3)
<pre>
sudo apt-get install python3-venv

cd <working_directory>
python3 -m venv foobar
source foobar/bin/activate
deactivate

sudo apt-get update
pip install --upgrade awscli
aws --version

sudo apt-get install software-properties-common
sudo apt-add-repository universe
sudo apt-get update
sudo apt-get install python3-pip
pip3 install boto3
</pre>

# How to install git using yum
<pre>
$ sudo yum install git
$ git --version
</pre>

# How to install git client using apt-get
TBD

# How to install AWS CLI version 2 in normal environment
<pre>
First, you will need to uninstall a prior version if it exists

Depending on how awscli was installed:

Option 1) pip uninstall awscli
Option 2) sudo find / -name aws  
          sudo rm path_of_aws_binary

After uninstalling any prior version of awscli, you can install the latest:

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install -i /usr/local/aws-cli -b /usr/local/bin   
aws --version

If you get the message: -bash: /home/ubuntu/.local/bin/aws: No such file or directory
then create a permanent symbolic link to /usr/local/bin/aws like so:

sudo ln -s /usr/local/bin/aws /home/ubuntu/.local/bin/aws

To update, repeat the steps above.
</pre>

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
$ df -i           list inode information instead of block usage
$ df -h           human readable

Start from root directory and issue:
$ sudo du -sh /*

To show hidden files, 
$ du -cksh .[!.]* * |sort -h

Or, install ncdu
$ sudo apt-get install ncdu
$ cd /  (navigate to root directory so you can search entire drive)
$ ncdu  <-- Super cool tool

Useful navigation keys:
o ?                      get list of all commands
o vim move commands      j|k|l|m
o g                      show percentage and/or graph
o s                      sort by size (default)
o n                      sort by name
o d                      delete file

Some good places to start are:
1) /var directory (if this is a Confluence/JIRA server)
2) /usr/src (if this is an ec2 instance, look for stale linux-aws-headers-x.x.x-xxxx binaries then issue `sudo apt update && sudo apt full-upgrade` followed by `sudo apt autoremove` to clean them out) 
2.1) alternatively, you can use --> sudo apt-get -y autoremove && sudo apt-get -y autoclean  OR sudo apt autoremove --purge 
2.notes) https://askubuntu.com/questions/1141630/why-is-usr-src-linux-aws-headers-growing

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

# Issue with AWS SageMaker video player not showing video properly in the task preview
<pre>
Symptoms: 
o video doesn't play properly in task preview
o video plays fine locally when downloaded from S3

Resolution:
Convert video to h.264 and re-upload to S3 
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

# Parameter Store Policy Example
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "VisualEditor0",
      "Effect": "Allow",
      "Action": [
        "ssm:PutParameter",
        "ssm:DeleteParameter",
        "ssm:GetParameterHistory",
        "ssm:GetParametersByPath",
        "ssm:GetParameters",
        "ssm:GetParameter",
        "ssm:DeleteParameters"
      ],
      "Resource": "arn:aws:ssm:us-east-1:123456789012:parameter/foobar-*"
    },
    {
      "Sid": "VisualEditor1",
      "Effect": "Allow",
      "Action": "ssm:DescribeParameters",
      "Resource": "*"
    }
  ]
}

AWS CLI: aws ssm get-parameter --name ssm_parameter_name_goes_here 
</pre>

# AWS Sagemaker CORS Configuration
<pre>
According to AWS documentation [https://docs.aws.amazon.com/sagemaker/latest/dg/sms-cors-update.html], 
all input data buckets will have to have CORS enabled starting Feb. 10th, 2021.


[
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "GET",
            "PUT",
            "HEAD"
        ],
        "AllowedOrigins": [
            "*"
        ],
        "ExposeHeaders": [
            "Access-Control-Allow-Origin"
        ],
        "MaxAgeSeconds": 3000
    }
]

</pre>


# S3 IAM Policy Examples
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ListBucketGetObject",
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket",
        "s3:GetObject",
        "s3:PutObject",
        "s3:DeleteObject"
      ],
      "Resource": [
        "arn:aws:s3:::bucket_name",
        "arn:aws:s3:::bucket_name/*"
      ]
    },
    {
      "Sid": "ListAllMyBucketsHeadBucket",
      "Effect": "Allow",
      "Action": [
        "s3:ListAllMyBuckets",
        "s3:HeadBucket"
      ],
      "Resource": "*"
    }
  ]
}
</pre>

<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowPutObject",
      "Effect": "Allow",
      "Action": [
        "s3:PutObject",
        "s3:PutObjectAcl"
      ],
      "Resource": [
        "arn:aws:s3:::bucket_name/data_collection_logs_ripped/*",
        "arn:aws:s3:::bucket_name/data_collection_validation_logs/*",
        "arn:aws:s3:::bucket_name/field_tests/*"
      ]
    },
    {
      "Sid": "ListBucket",
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::bucket_name"
      ]
    }
  ]
}
</pre>

<pre>
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ScopeToBucketOnly",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:ListBucket",
                "s3:DeleteObject"
            ],
            "Resource": [
                "arn:aws:s3:::bucket_name/*",
                "arn:aws:s3:::bucket_name"
            ]
        },
        {
            "Sid": "RestrictListBucketsToS3BucketName",
            "Effect": "Allow",
            "Action": [
                "s3:ListAllMyBuckets",
                "s3:HeadBucket"
            ],
            "Resource": "*",
            "Condition": {
                "StringLike": {
                    "s3:prefix": "bucket_name"
                }
            }
        }
    ]
}
</pre>

# S3 - How to get the largest items in an S3 bucket
<pre>
Example:
aws s3api list-object-versions --bucket BUCKETNAME | jq -r '.Versions[] | "\(.Key)\t \(.Size)"' | sort -k2 -r -n | head -10

Resource: 
https://www.cloudsavvyit.com/7894/how-to-get-the-largest-items-in-an-s3-bucket/
</pre>

# S3 MultipartUpload Notes
<pre>

Error
An error occurred (AccessDenied) when calling the CreateMultipartUpload operation: Access Denied

Required Permissions
s3:PutObject
s3:GetObject
s3:ListBucketMultipartUploads
s3:ListMultipartUploadParts

If bucket policy requires --acl bucket-owner-full-control be set then required permission is
s3:PutObjectAcl

Multipart threshold can also be tuned like so in CLI 
s3 =
   max_concurrent_requests = 100
   max_queue_size = 10000
   multipart_threshold = 64MB <---
   multipart_chunksize = 16MB
   max_bandwidth = 4096MB/s
</pre>

# S3 Stream Logger
<pre>
AWS support has tools to dig deeper into S3 permission failures but this requires verbose debugging.
When using the CLI, you can use the --debug option to extract the S3 Request ID.
With Boto3, you can add the following line --> boto3.set_stream_logger('boto3.resources', "")
Just note, the "" can expose sensitive information so don't use this in a production environment.
</pre>

# S3 ListObjects Failure Due to Request Payer Enabled on Bucket
<pre>
If your bucket has requester pays enabled then user from other accounts should specify request-payer parameter when they send request to the bucket otherwise the bucket throws "Access Denied" error. This is how S3 indirectly forces the user to send the requester payer header as otherwise it denies the request on a requester pays enabled bucket.
To check if Requester Pays is enabled, you can use the Amazon S3 console to view your bucket’s properties.

The following example AWS CLI command includes the correct parameter to access a bucket with Requester Pays:

aws s3 ls s3://awsexamplebucket --request-payer requester
</pre>

# S3 IAM Policies for IAM users
<pre>
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Statement1",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:PutObjectAcl",
                "s3:GetObject",
                "s3:GetObjectAcl",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::bucket_name_goes_here/*",
                "arn:aws:s3:::bucket_name_goes_here"
            ]
        }
    ]
}
</pre>




# S3 Bucket Policy Examples
https://docs.aws.amazon.com/AmazonS3/latest/dev/example-bucket-policies.html#example-bucket-policies-use-case-8

# Basic template for IAM identities
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Statement1",
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::account_number:user/david",                          # IAM user
                    "arn:aws:iam::account_number:root",                                # AWS account
                    "arn:aws:iam::account_number:role/role_name_goes_here",            # IAM role
                ]
            },
            "Action": [
                "s3:PutObject",
                "s3:PutObjectAcl",
                "s3:GetObject",
                "s3:GetObjectAcl",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::bucket_name_goes_here/*",
                "arn:aws:s3:::bucket_name_goes_here"
            ]
        }
    ]
}
```

# Basic template for AWS SSO UserIds
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Deny All Users except those permitted",
            "Effect": "Deny",
            "Principal": "*",
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::bucket_name/*",
                "arn:aws:s3:::bucket_name"
            ],
            "Condition": {
                "StringNotLike": {
                    "aws:userid": [
                        "AROA5QXRKRKPBI4HCTKFM:SSOUsername",     # Example SSO user
                        "AIDAJR6UPPDJO7O5IJNHM",                 # IAM user?
                        "AROAJBWNRJTSH4UD7N2LA:CloudCustodian"   # IAM role?
                    ]
                }
            }
        }
    ]
}

 
```

# How to configure basic read/write access to S3 bucket prefix for IAM user
<pre>
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "S3ReadWriteAccess",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::ACCOUNT_NUMBER:user/USERNAME"
            },
            "Action": [
                "s3:Get*",
                "s3:List*",
                "s3:Put*"
            ],
            "Resource": [
                "arn:aws:s3:::BUCKETNAME/PREFIX*",
                "arn:aws:s3:::BUCKETNAME"
            ]
        }
    ]
}
</pre>

If the IAM user is from a cross-account, then that user will require an IAM policy as well
<pre>
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "S3ReadWriteAccess",
            "Effect": "Allow",
            "Action": [
                "s3:Get*",
                "s3:List*",
                "s3:Put*"
            ],
            "Resource": [
                "arn:aws:s3:::BUCKETNAME/PREFIX",
                "arn:aws:s3:::BUCKETNAME"
            ]
        }
    ]
}
</pre>


# How to enforce cross account s3:Put* access to S3 bucket with --acl bucket-owner-full-control set
<pre>
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Cross Account Put Access",
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::111111111111:user/david.lin",
                    "arn:aws:iam::222222222222:root"                
                ]
            },
            "Action": "s3:Put*",
            "Resource": [
                "arn:aws:s3:::BUCKETNAME/*",
                "arn:aws:s3:::BUCKETNAME"
            ],
            "Condition": {
                "StringEquals": {
                    "s3:x-amz-acl": "bucket-owner-full-control"
                }
            }
        },
        {
            "Sid": "Cross Account Read Access",
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::929292782238:user/david.lin.ctr",
                    "arn:aws:iam::222222222222:root"
                ]
            },
            "Action": [
                "s3:Get*",
                "s3:List*"
            ],
            "Resource": [
                "arn:aws:s3:::BUCKETNAME/*",
                "arn:aws:s3:::BUCKETNAME"
            ]
        }
    ]
}
</pre>

# How to enforce --acl bucket-owner-full-control based on orgID 
<pre>
{
    "Version": "2012-10-17",
    "Id": "lakehouse-s3-access-pipeline-managed",
    "Statement": [
         {
            "Sid": "PutObjectCondition",
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::ACCOUNT_ID_A:root",
                    "arn:aws:iam::ACCOUNT_ID_B:root"
                ]
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::BUCKETNAME_GOES_HERE/*",
            "Condition": {
                "StringEquals": {
                    "s3:x-amz-grant-full-control": "id=CANONICAL_ID_OF_BUCKET_ACCOUNT"
                }
            }
        },
        {
            "Sid": "OtherOrgLevelActions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": [
                "s3:GetObject",
                "s3:ListBucket",
                "s3:PutBucketACL",
                "s3:PutObjectACL"
            ],
            "Resource": [
                "arn:aws:s3:::BUCKET_NAME_GOES_HERE",
                "arn:aws:s3:::BUCKET_NAME_GOES_HERE/*"
            ],
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalOrgID": "o-xxxxxxxxxx" (PrincipalOrgID goes here)
                }
            }
        }
    ]
}

Note: When using the condition containing PrincipalOrgID, you can use a wildcard as the Principal.
      When using the condition containing string s3:x-amz-grant-full-control, you must specify an IAM user/role arn
      that resides in the account based on the Canonical ID. 
</pre>

# How to restrict access to S3 bucket by IAM user/roles (aka UserId and RoleId) in S3 Bucket Policy 
<pre>
Example bucket policy

        {
            "Sid": "DenyS3WriteAccessExceptAllowedList",
            "Effect": "Deny",
            "Principal": "*",
            "Action": [
                "s3:PutObject",
                "s3:DeleteObjectVersion",
                "s3:PutObjectVersionAcl",
                "s3:DeleteObject",
                "s3:PutObjectAcl"
            ],
            "Resource": [
                "arn:aws:s3:::foo/1",
                "arn:aws:s3:::foo/1/*",
                "arn:aws:s3:::foo/2",
                "arn:aws:s3:::foo/2/*"
            ],
            "Condition": {
                "StringNotLike": {
                    "aws:userId": [
                        "111111111111",              <---- AWS account ID
                        "AROAIJTBUZHPXHCA4IQ3U:*",   <---- IAM role ID via CLI "aws iam get-role --role-name ROLE-NAME"
                        "AIDAJ5XNA27JE4PZE55FC"]     <---- IAM user ID via CLI "aws sts get-caller-identity"
                }
            }

Read more: https://aws.amazon.com/blogs/security/how-to-restrict-amazon-s3-bucket-access-to-a-specific-iam-role/
</pre>


# S3 Bucket Policy for Cross Account Actions That Requires Principals to use the option --acl bucket-owner-full-control
Use the following on the destination bucket
<pre>
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Account Access",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::929292782238:user/david.lin"
            },
            "Action": [
                "s3:Get*",
                "s3:Put*",
                "s3:List*"
            ],
            "Resource": [
                "arn:aws:s3:::BUCKET_NAME/*",
                "arn:aws:s3:::BUCKET_NAME"
            ]
        },
        {
            "Sid": "RefuseAllPutsFromOtherAccountsWithoutFullControlACL",
            "Effect": "Deny",
            "Principal": {
                "AWS": "*"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::BUCKET_NAME/*",
            "Condition": {
                "StringNotEquals": {
                    "s3:x-amz-acl": "bucket-owner-full-control"
                }
            }
        }
    ]
}
</pre>

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

Basic read only access for cross accounts
<pre>
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AccountListAccess",
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::111111111111:root"
                ]
            },
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::BUCKETNAME"
        },
        {
            "Sid": "AccountGetAccess",
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::111111111111:root"
                ]
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::BUCKETNAME/*"
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

# AWS IAM Billing Full Access Policy
<pre>
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "account:*",
                "aws-portal:*",
                "pricing:*",
                "cur:*",
                "budgets:*",
                "ce:*"
            ],
            "Resource": "*"
        }
    ]
}
</pre>

# S3 Update ACL for all objects in folder with bucket-owner-full-control
<pre>
Recusively
aws s3 cp s3://bucketname/folder1/ s3://bucketname/folder1/ --recursive --acl bucket-owner-full-control --metadata updated=$(date)

Per object
aws s3api put-object-acl --bucket destination_bucket_name --key bucket_prefix --acl bucket-owner-full-control
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

# AWS CLI with JMESPATH Queries 
```
#!/bin/bash -ex
export AWS_REGION=your-region-here
export AWS_PROFILE=your-cli-access-profile-here
export AWS_DEFAULT_OUTPUT=text

# Get your user ARN
aws iam get-user --query 'User.Arn'

# Get the list of key pairs available to an account sorted alphabetically
aws ec2 describe-key-pairs \
  --query 'KeyPairs[*].[KeyName] | sort(@)'

# List account role ARNs
aws iam list-roles --query 'Roles[].Arn'

# List instance ID's by name tag using filter
aws ec2 describe-instances \
  --filter 'Name=tag:Name,Values=instance-name-here' \
  --query 'Reservations[*].Instances[*].InstanceId'

# Create a volume from a snapshot ID and get the resulting volume ID
aws ec2 create-volume \
  --snapshot-id snap-id \
  --encrypted true \
  --availability-zone az \
  --query VolumeId

# List the available set of server cert ARNs
aws iam list-server-certificates \
  --query 'ServerCertificateMetadataList[*][Arn]'

# Get the first Cloudformation stack and return a specific output key value
aws cloudformation describe-stacks \
  --query "Stacks[0].Outputs[?OutputKey=='key'].OutputValue"

# Get AMIs that are available and have a substring in their name
aws ec2 describe-images \
  --filters Name=name,Values=*-name-contains-* Name=state,Values=available \
  --query 'Images[*].[ImageId,Name] | sort(@)'

# Get available Cloudformation stacks, sort by age
aws cloudformation list-stacks \
  --query 'StackSummaries[?StackStatus==`CREATE_COMPLETE`].[CreationTime,StackName] | sort(@)'

# Get the private IPs of a set of instances based on a shared tag*
# *only useful if you're expecting the instance to have only one ENI.
aws ec2 describe-instances \
  --filter Name=tag:Name,Values=tag \
  --query 'Reservations[*].Instances[].[NetworkInterfaces[0].PrivateIpAddress]'

# List record sets
aws route53 list-resource-record-sets \
  --hosted-zone-id id \
  --query 'ResourceRecordSets[*].[Name]'

# Get the availability zones of VPC subnets
aws ec2 describe-subnets \
  --query 'Subnets[*].[VpcId,SubnetId,AvailabilityZone]'

# Get the volume ID of an instance knowing the mount point and instance ID
aws ec2 describe-volumes \
  --filters Name=attachment.instance-id,Values=instance-id \
  --query 'Volumes[*].Attachments[?Device==`/dev/sdh`].VolumeId'

# Get the userdata of an EC2 instance
aws ec2 describe-instance-attribute \
  --attribue userData \
  --instance-id instance-id \
  --query 'Userdata.Value' | base64 --decode

# Get account security groups and format the output as JSON
aws ec2 describe-security-groups \
  --query SecurityGroups[*].{ID: GroupId}

# Get the first security group ID alphabetically
aws ec2 describe-security-groups \
  --query 'SecurityGroups[*].GroupId | sort(@) | [0]'
```

# How to use GIMP to create an avatar
<pre>
Windows --> Single-Window mode
Open jpg image
Bottom of screen --> select 12.5% (or appropriate zoom value)
Crop tool + Shift (to fix square) --> Enter
Image --> Rescale Image  (for Atlassian use 500x500 px)
File --> Export as --> give jpg new descriptive name --> Export
</pre>

# How to strip characters from aws s3 ls command using cut
<pre>
$ aws s3 ls | cut -c 20-        This displays everything to the right starting at the 20 character
$ aws s3 ls | cut -c 20        This displays the first 20 characters of each line

This approach can also be used for other simple output.
</pre>

# How to prevent creation of AWS IAM users with email based usernames
<pre>
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Deny",
            "Action": "iam:CreateUser",
            "Resource": "arn:aws:iam::*:user/*@*"
        }
    ]
}
</pre>


# How to use inxi to get system info
<pre>
Installation
sudo apt-get install inxi
sudo yum install inxi

+------------------+--------------------------------------------------------------------+
| Command          | Description                                                        |
|------------------+--------------------------------------------------------------------|
| sudo inxi -F     | semi-full summary overview of all info about your system           |
|------------------+--------------------------------------------------------------------|
| sudo inxi -C     | CPU information                                                    |
|------------------+--------------------------------------------------------------------|
| sudo inxi -CfxCa | full overview of all information for CPU including vulnerabilities |
|------------------+--------------------------------------------------------------------|
| sudo inxi -m     | Memory information                                                 |
|------------------+--------------------------------------------------------------------|
| sudo inxi -D     | Disk information                                                   |
|------------------+--------------------------------------------------------------------|
| inxi -w          | Weather information                                                |
+------------------+--------------------------------------------------------------------+

Man Page
man inxi

CloudSavvy Article:  https://www.cloudsavvyit.com/8123/the-linux-system-information-tool-inxi/
Official Repository: https://github.com/smxi/inxi
</pre>

# How to test cross account access to ECR repository using AWS profile
<pre>
1) On a test machine, setup ~/.aws/config with a test cross account profile

Example:
[profile foobar]
region = us-east-1
output = json
role_arn = arn:aws:iam::123456789012:role/OrganizationAccountAccessRole
source_profile = default

2) Update the ECR repository permission to allow the cross account ID

Example:
{
  "Version": "2008-10-17",
  "Statement": [
    {
      "Sid": "AllowCrossAccountPullForVspiritBuildEnv",
      "Effect": "Allow",
      "Principal": {
        "AWS": [
          "arn:aws:iam::$CROSS_ACCOUNT_ID:root"   <--- Replace $CROSS_ACCOUNT_ID with cross account ID
        ]
      },
      "Action": [
                "ecr:BatchCheckLayerAvailability",
                "ecr:BatchDeleteImage",
                "ecr:BatchGetImage",
                "ecr:CompleteLayerUpload",
                "ecr:DescribeImages",
                "ecr:DescribeRepositories",
                "ecr:GetDownloadUrlForLayer",
                "ecr:GetRepositoryPolicy",
                "ecr:InitiateLayerUpload",
                "ecr:ListImages",
                "ecr:PutImage",
                "ecr:UploadLayerPart",
                "ecr:GetAuthorizationToken"
        ]
    }
  ]
}

3) On cross account side, attach IAM policy to appropriate principal that mirrors the ECR resource permissions above
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "ecr:BatchCheckLayerAvailability",
                "ecr:BatchDeleteImage",
                "ecr:BatchGetImage",
                "ecr:CompleteLayerUpload",
                "ecr:DescribeImages",
                "ecr:DescribeRepositories",
                "ecr:GetDownloadUrlForLayer",
                "ecr:GetRepositoryPolicy",
                "ecr:InitiateLayerUpload",
                "ecr:ListImages",
                "ecr:PutImage",
                "ecr:UploadLayerPart",
                "ecr:GetAuthorizationToken"
            ],
            "Resource": "arn:aws:ecr:us-east-1:123456789012:repository/myawesomerepository"
        }
    ]
}

4) Verify docker is installed on test machine

Example:
$ docker run hello-world

5) Generate a temporary Docker authentication token from the secondary account

Example:
$ aws ecr get-login-password --profile foobar --region us-east-1 | docker login --username AWS --password-stdin $SOURCE_ACCOUNT_ID.dkr.ecr.us-east-1.amazonaws.com

Note the --profile option is used, the region (us-east-1) must match and that $SOUCE_ACCOUNT_ID is the account number where the ECR repository lives.
If any changes are made to the ECR repository permissions (e.g. account number(s) and/or actions added/removed), then you need to generate a new temporary Docker auth token.

6) Perform a test push or pull

Example:
$ docker pull $ECR_REPO_URI

The ECR repo URI can be obtained from the management console.
$ docker pull 123456789012.dkr.ecr.us-east-1.amazonaws.com/myawesomeimage:20210415ksg-tothemoon

Resource: (Link)[https://aws.amazon.com/premiumsupport/knowledge-center/secondary-account-access-ecr/]
</pre>

# AWS SSO + AWS CLI 
<pre>
o AWS SSO requires AWS CLI v2.0 or higher
  To install, open PowerShell window and isssue: 
  msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi

o ~/.aws/config File Example
[default]
region = us-east-1

[profile default]
sso_start_url = https://acmecorp-sso.awsapps.com/start
sso_region = us-east-1
sso_account_id = {account_number}
sso_role_name = AdministratorAccess
region = us-east-1
output = json

Note: The AWS config/credential files are stored under %UserProfile% in Windows (e.g. C:\User\YourName)

o To login/logout:
aws sso login
aws sso logout

Note: 
To configure an AWS SSO profile dynamically, issue aws configure sso.
To configure a group of AWS SSO profiles manually, run the shell script named sso_profiles.sh in your scripts repo and save over ~/.aws/config.
To refresh your token seesion for a given profile, issue aws sso login --profile profile_name.
</pre>

# IAM Policy Allowing IAM User to PassRole to an AWS Service
<pre>
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "",
            "Effect": "Allow",
            "Action": [
                "iam:PassRole",
                "iam:GetRole"
            ],
            "Resource": "arn:aws:iam::123456789012:role/role_name_goes_here"
        }
    ]
}
</pre>

# AWS Service Control Policy (SCP) Examples

DenyECService
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "NotAction": "ec2:DescribeInstances",
      "Resource": "arn:aws:ec2:*:*:instance/*",
      "Condition": {
        "ArnEquals": {
          "aws:PrincipalARN": [
            "arn:aws:iam::123456789012:*"
          ]
        }
      }
    }
  ]
}
</pre>

DenySagemakerService
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "sagemaker:*"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
</pre>
