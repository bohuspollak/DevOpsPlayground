prerequisite: Git Bash https://gitforwindows.org/ 

reference: https://help.github.com/en/articles/adding-an-existing-project-to-github-using-the-command-line

# initial commit from project directory
git init
git config --global user.name "Name Surname"
git config --global user.email email@email.email
git add README.md
git commit -m "initial commit"
git remote add origin https://github.com/bohuspollak/DevOpsPlayground.git
git push -u origin master
git add -A
git config --global user.name "Name Surname"
git config --global user.email email@email.email
git commit -m "adding structure and files"
git push -u origin master
git status

Reference: https://www.jetbrains.com/help/idea/manage-projects-hosted-on-github.html

VCS->Checkout From VCS -> Git
URL: https://github.com/xxxx/xxxxx.git
Directory: C:\projects\DevOpsClone (enter non existing directory)
Confirm opening

## ignoring files
Add to Intellij Plugins: Add to gitignore
vi .git/info/exclude
TODO correct regexp

## clone repo
Start git bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY
cd YOUR-REPOSITORY
git status


