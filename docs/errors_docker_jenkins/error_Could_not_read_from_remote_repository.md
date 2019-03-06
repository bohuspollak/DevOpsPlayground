When executing:
git push docker_git_server --set-upstream master

#error: user@localhost: Permission denied (publickey,keyboard-interactive).
#fatal: Could not read from remote repository.

/home/user/.ssh/config
host localhost
 HostName localhost
 Preferredauthentications publickey
 IdentityFile /c/cygwin64/home/user/.ssh/id_rsa
 User jenkins
 LogLevel DEBUG


git push docker_git_server --set-upstream master
Solution: Setup config in home directory under .ssh/config
with IdentityFile not 
/home/user/.ssh/id_rsa 
but 
/c/cygwin64/home/user/.ssh/id_rsa
because of cygwin mapping of drive
You can see the file from cygwin but the git will not be able to access it for some reason under the short path.
