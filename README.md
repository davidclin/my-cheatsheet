# git-cheatsheet
My Git Cheatsheet

## Useful commands
<pre>
git clone
git add
git commit -m "message_goes_here"
git push
</pre>

## Other related commands
<pre>
git switch   (modern)                          replaces checkout command to switch between branches
git switch -c branch_name                      creates new branch and switches to it
git checkout (old)                             
git checkout -- [., file_name]                 resets non-staged changes back to the last commit
</pre>

## Config related commands
<pre>
git config --list             shows all git configurations
git config user.name          shows username 
git config user.email         shows email address
git remote -v                 shows what origin (remote) is set to
git remote set-url origin git@github.com:davidclin/cheatsheet.git
</pre>

## How to setup your local ssh key
<pre>
cd ~/.ssh
touch david
add your ssh secret file to "david"
chmod 600 david
append following to ~/.bashrc or ~/.zshrc


eval "$(ssh-agent -s)"
ssh-add ~/.ssh/david
</pre>