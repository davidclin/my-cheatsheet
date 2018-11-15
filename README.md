# Cheatsheet
David's Cheatsheet and Examples

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

# How to find large files
<pre>
See disk utilization
$ df

Start from root directory and issue:
$ sudo du -sh *

Change into suspect directory and repeat command until you find source of large files.
</pre>
