- [Linux](#linux)
  - [Bash shell scripting](#bash-shell-scripting)
    - [Creating a shell script to create an nginx web server.](#creating-a-shell-script-to-create-an-nginx-web-server)
    - [Executing the bash script](#executing-the-bash-script)
    - [Creating a custom nginx webpage](#creating-a-custom-nginx-webpage)
  - [Additional Linux](#additional-linux)
    - [Creating my own environment variable:](#creating-my-own-environment-variable)
    - [Processes-](#processes-)
    - [To stop processes:](#to-stop-processes)
  - [Permissions-](#permissions-)
  - [Cloud Security](#cloud-security)



# Linux
- `code .` - Allows you to take that folder from git bash to vscode.
- `ls -la` - shows permissions of all files hidden ones too.
- `cd / ` - Takes you to the root directory.
- `cd ..` - Takes you to the parent directory (directory before).
- `cd ~` - Takes you to your home directory. By default should have full permissions to this directory.
  - There's also a home folder but its different to the home directory!
- `ls -a` shows hidden files.
- Once inside the vm, run these 
- `pwd` - print working directory.
- commands:
  - `sudo apt update -y`
    - Good to use to check if vm is connected to the internet. 
    - Sudo= super user do.
  - `sudo apt upgrade -y`
  
## Bash shell scripting
### Creating a shell script to create an nginx web server.
- `nano provision.sh`
  - Opens an editor and creates the shell file. 
  - Create the script inside this:
     ```
      #!/bin/bash
      #update
      sudo apt update -y

      #upgrade
      sudo apt upgrade -y

      #install nginx
      sudo apt install nginx -y

      #restart nginx
      sudo systemctl restart nginx

      #enable nginx - enabled - starts automatically when we restart virtual machine.
      sudo systemctl start nginx
      sudo systemctl enable nginx
      #Check if its enable: sudo systemctl is-enabled nginx
      ```
  - The **#!/bin/bash**:
    - A path to the bash interpretor - tells it how to interpret the commands. 

### Executing the bash script
- `chmod +x /home/adminuser/provision.sh && ./provision.sh`
- This gives executable permissions to every user for that file and then also runs the script.
- `./provision.sh` - executes the script.
- Can't execute any file without the correct permissions.
- 

If you make a change to nginx, you need to restart it before those changes are applied.
systemctl controls system processes e.g. installed tools/services.

### Creating a custom nginx webpage

  To backup the default:
  - sudo cp -r /var/www/html /var/www/html_backup
  - Copies the entire html folder to a new folder called html_backup in the www folder.
  -  -r flag copies everything in that html folder including the files and subfolders.

- Create an index.html file in the /**var/www/html** directory `sudo nano index.html`
- Enter this in the index.html file:

```
- This code generates a web page.
<!DOCTYPE html>
<html>
<head>
    <title>My Web Page</title>
</head>
<body>
    <h1>Welcome to Zainab's webpage!</h1>
</body>
</html> 
```


To download the image first:
- `sudo wget https://c02.purpledshub.com/uploads/sites/40/2023/08/JI230816Cosmos220-6d9254f-edited-scaled.jpg`
- Another way to download image - ` curl https://cdn.britannica.com/39/7139-050-A88818BB/Himalayan-chocolate-point.jpg --output cat.jpg
`
  - The curl command requires the name at the end with --output flag.


Upgraded version with an image link:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Web Page</title>
</head>
<body>
    <h1>Welcome to Zainab's webpage!</h1>
    <p>Here is a beautiful flower:</p>
    <img src="JI230816Cosmos220-6d9254f-edited-scaled.jpg
" alt="A beautiful flower" style="width:300px; height:auto;">
</body>
</html>
```

## Additional Linux

- `sed` - finds something in a file and replaces it for you.
- `mv` = Renames files and also moves files. 
  - `mv cat.jpg cat.txt` = Changes name of jpg file to a txt file.
  - The file is still seen as a jpg file - can't trick linux.
  - To move a file to a different folder `mv filename existingFolderName`.
  - Another way to move file to home directory `mv chicken-joke.txt /home/adminuser/`
  - `mv /home/adminuser/funny-stuff/chicken-joke.txt ~` = moving a file even if you don't cd to the location of the file - just add the paths.
- `file cat.jpg` = shows file details e.g. what kind of file it is. 
- `rm` = deletes files. 
- `mkdir` = creates a folder  
  - If you add a space in between the folder name it will create 2 folders so don't use space. 
  - If you want a space, use quotes.
    - e .g "my pictures" - to cd into this folder you have to use quotes too.
- `rm -r` = Removes a directory even with files in it.
- `rm -rf` = deletes folder forced even when theres contents - dangerous.
- `rmdir` = removes directory if its empty (safer).
- `touch` = Creates an empty file.
- `cat` = Dumps contents of file on the screen.
- `nano` = file editor.
- `head -2 chicken-joke.txt` = Gives you the first 2 lines in the file.
- `tail -2 chicken-joke.txt` = Gives you the last 2 lines in the file.
  - Both head and tail will output 10 lines if number not specified.
- `nl` = numbers all the lines of the files. 
- `grep` =  `cat chicken-joke.txt | grep chicken`
  - Finds the word you're looking for - filters the file for specific information.
- Installing tree = `sudo apt install tree` 
  - Good for folder and file structure. 
  - Use command `tree` to see the structure of files in a better way.
- `sudo !!` = Runs your previous command with sudo (root permissions) if you previously didn't use sudo.
- `grep -r chicken` = Also filters files for the word chicken.
- `sudo su` = root user access to run multiple commands with root permissions- dont have to use sudo.
- `>>` = append files.

Environment variables- 
  - Variables contain data (atleast one piece of data).
  - Good way for an application to access something sensitive.
  - Linux env variables are case sensitive.

- `printenv` - prints all variables.
- `printenv USER` - prints the specific environment variable.
### Creating my own environment variable:
- `MYNAME=zainab` = This just creates a variable not an environment variable.
- `echo $MYNAME` = Prints the name.
  - Always have to use $ for variables.
  
To create it as an environment variable: `export MYNAME=zainab` 
- If you exit vm, and ssh back in, the env variable disappears. (no persistance).

Making the env variable persistent: Only works for the user you change the bashrc file for.
- `echo "export MYNAME=zainab_is_persistent"` - Just prints the command.
- `echo "export  MYNAME=zainab_is_persistent" >>.bashrc` - same command but uses `>>` to add the echo comment to the .bashrc file.
  - The .bashrc file is persistent.
- ` tail -3 .bashrc` - Prints the last 3 lines of the file to prove that it's appended with the command comment.
- ` source .bashrc` - refreshes the file- because it runs on start of vm so when refreshed it runs and it should run the command that was added to it since its a script file.
- ` printenv MYNAME` - Should now show the env variable.
- `exit` and ssh back into the vm- `printenv MYNAME` again and should still see the variable as it's in a persistent directory.




### Processes- 
- User processes (`ps`)
- Sytem processes (`ps -e`)
- **`ps -aux`** - detailed process overview.
- `top`- Refreshes every 3 seconds- real-time.
  - Orders the processes.
  - Top of the list is ranked by amount of cpu being used.
  - SHIFT + N = most memory
  - SHIFT + P = most cpu

`sleep 3` - makes your terminal sleep for 3 seconds. 
`sleep 5000 &` - Runs command in the background.
  - `jobs` - You can see the processes running in the background.
  - `jobs -l` - shows ID too.
  
`sudo systemctl status nginx` - Checks status of the process nginx.
`stop nginx` - Stops the process. 

### To stop processes:
  - `kill` - Different levels.
  - **The gentlest**= `kill -1 2990`
    - 2990= process ID (find by using `jobs -l).
    - Called a hang up.
  - **Medium level**= `kill -15`
    - Terminate.
    - Graceful- Terminates any child processes first and then kills any parent processes.
    - It's the default so can also just put `kill` with process ID.
  - **Strongest level of kill**= `kill -9 <processID>` 
    - Harshest form of kill.
    - It will kill the parent process. The child processes will become zombie processes- they'll be left running in memory. Won't cause harm but needs manual clean up if dont need them. 
  
pm2= Process manager. 
  - Going to start up a child process for us to run an application (nodeJS app).
    - If you kill that child process, it will instantly start up another child process for that application to stay running. This is because it's responsible for keeping the app alive.
    - Want to shut down the process= Gracefully terminate it. 


## Permissions- 
- `sudo` - good for one time commands - cannot access environment variables 
- `chown` - change owner
- `chmod 777` - read and write and execute permissions.
- `sudo -E` - to access the environment variables too.

## Cloud Security

Is security better in the cloud than on-prem - 
- Possible to make security mistakes on cloud and on prem.
- Depends on the effort put in.
- Depends on the model you use:
  - IAAS: more responsibility of security. 
  - PAAS: less responsibility of security. More managed- less patching required.