Setting up local and remote Git repositories:

 
1. You have a working folder/directory on your local computer, which is called for example:
project_one

You want to be able to push the changes to your remote github repository located on https://github.com/
You have an account there, my account's username is Homap.

2. Create a repository on github website by clicking on "Repositories", then on "New", choose a name for your Repository and create your repository without README. Mine is called algae_nanopore

3. Now, in your local directory called project_one, initialise git:
git init

4. If you want to add the content of whole directory project_one to git, do:
git add . && git commit -m "adding project one to git"

5. If you want to add only a specific directory such as the code directory within project_one: (Github cannot accept files larger than 100 Mb so not advisable to add the data directory if containing large files)
git add code && git commit -m "code for this study"

6. In terminal add the URL of the remote repository where the local will be pushed to, for example I called my remote repository on github algae_nanopore
git remote add origin https://github.com/Homap/algae_nanopore.git

7. Check if it has been added
git remote -v

8. Create ssh key. ssh key allows you to access remote servers without needing to supply your username and password every single time. To do that, you need to use the email you used to create your Github account, mine is my gmail: 
ssh-keygen -t ed25519 -C "hpapoli@gmail.com"

9. You will get the command line prompt which asks you where to store your key and what to call it. It's useful to choose a unique name for each project you have as you might have many github projects and you want to be specific which one you push to. By default, it stores the ssh key in your home directory, my home is /home/homap and by default the key is called  id_ed25519 but I want to call my ssh key for this project id_ed25519_algae_nanopore
Enter file in which to save the key (/home/homap/.ssh/id_ed25519): /home/homap/.ssh/id_ed25519_algae_nanopore

10. You are then prompted to set a password

11. Now you need to add the ssh key to the remote repository. To do that, copy the content of file 
/home/homap/.ssh/id_ed25519_algae_nanopore.pub 

then go to the github repository on Github website, under Settings, Deploy keys, Add deply key, paste the content and check "Allow write access".

12. Now the key is added to your github. Activate the ssh-agent in your local repository in Terminal: 

eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519_algae_nanopore

13. Rename the new branch main

git branch -M main

14. Finally push the changes to your github account to the main branch

git push -u origin main

15. You are all set now. Keep working on your project and every now and then add your changes to git and push them to github as follows:
git add code/lala.py && git commit -m "made 3 changes to lala"
git push -u origin main

16. It's been weekend and you are starting a new session after getting back to your project. You need to re-activate the ssh-agent to save yourself from having to enter username and password every time:
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519_algae_nanopore

 
And that's it! 🎉

* Common error: When entering the last command "git branch -M main" on an empty directory, you get the error:
error: refname refs/heads/master not found
fatal: Branch rename failed

The fix is easy! Just add an empty file to the directory you'd like to push to github like this:
touch project_one/code/README.md
git add code && git commit -m "adding my codes"

Run the commands again and all should work fine:
git branch -M main
git push -u origin main
