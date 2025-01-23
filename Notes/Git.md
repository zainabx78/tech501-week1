# Git

* Saves versions of files/folders.
* Tracks changes.

## Git repository (Repo)
* Just a normal folder/directory at the beginning.
* Use git init to turn the folder into a git repository.

### Changing the name of the master branch
* Use [git branch -M main] to change the name of the master branch to main. 
* The default branch is now called main. (The way github likes it).
## 3 States of Git
1. Modified (same as untracked) - This shows the file as red when git status command is ran.
2. Staged (same as tracked and added to index) - This shows the file as green when git status command is ran. To get a file to this stage, need to run [git add .]
3. Committed - To get a file to this stage, need to run [git commit -m "message"]. This Shows the "status as working tree clean"

# GitHub

## Syncing the local git repo to your gitub repo.
- In the git bash terminal, in the repo folder, enter the command: **[git remote add origin https://github.com/zainabx78/tech501-week1-.git].**
  - This command links your local repo to the github repo.
- Then push the commits to the github repo- actual syncing **[git push -u origin main].**
- Only need to specify the branch name the first time you push. Next time can just use command **[git push]**
- Only the changes you've committed will be synced up. 
- Opposite of push command is the git pull command. When you want to sync changes from github repo to the local repo. 
  