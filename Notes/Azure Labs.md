- [Azure Cloud](#azure-cloud)
    - [Good practices:](#good-practices)
  - [Creating a VM inside a Vnet and entering it through SSH](#creating-a-vm-inside-a-vnet-and-entering-it-through-ssh)
    - [To create a keypair:](#to-create-a-keypair)
    - [Adding the key onto Azure cloud](#adding-the-key-onto-azure-cloud)
    - [Creating a vnet](#creating-a-vnet)
    - [Creating a VM](#creating-a-vm)
    - [SSH into the VM](#ssh-into-the-vm)
    - [Deleting resources](#deleting-resources)
- [Linux](#linux)
  - [Bash shell scripting](#bash-shell-scripting)
    - [Creating a shell script to create an nginx web server.](#creating-a-shell-script-to-create-an-nginx-web-server)
  - [Creating a custom nginx webpage](#creating-a-custom-nginx-webpage)


#  Azure Cloud
### Good practices:

- Naming conventions- Add the actual resource name at the end of the name. E.g If you're creating a vnet, name it **tech501-zainab-test-vnet**.
- Tags- Name:Owner and Value:Zainab.

Virtual machines live in virtual networks (vnets). Also require subnets. 

Public Ip addresses cost money. They're also optional. Private IP addresses are allocated to the VM's from the subnet CIDR block. 

## Creating a VM inside a Vnet and entering it through SSH
### To create a keypair:

- ~ = home directory. 
.ssh folder needs to exist in that. 
- [cd] Shortcut to get to home directory.
- Any file or folder starting with [.] is hidden. 

- To view hidden files/folders: [ls -a].
- change directories to be in the .ssh folder to create the keypair in. [cd .ssh]

- [ssh-keygen -t rsa -b 4096 -C "zainabfarooq001@gmail.com"]
  
- The public key generated will be put onto azure to use for the VM. 
- The private key will be used when you want to access the vm. 
### Adding the key onto Azure cloud
- Go to ssh keys in azure.
- Create ssh key. 
- Name the key the same as the key you created locally. 
- Select the add existing key option.
- Use [cat tech501-zainab-az-key.pub] in git bash to print your public key content. Copy and paste into the azure box.
- Add tag Name: Owner and Value: Zainab. 
### Creating a vnet
- Naming convention- tech501-zainab-2-subnet
- CIDR block- 10.0.0.0/16 (65,536 addresses).
- Create public subnet-
  - Edit default subnet 
  - Name: public-subnet
  - CIDR block: 10.0.2.0/24 (256 addresses)
- Add private subnet-
  - Name: private subnet
  - CIDR block: 10.0.3.0/24
  - Tags: Name:Owner, Value:Zainab 
### Creating a VM
- Go to azure virtual machine.
- Naming convention: tech501-zainab-first-vm.
- Image: Ubuntu Pro 18.04 LTS - x64 Gen2 [LTS means long term support for ~7 years].
- Size: Standard_B1s - 1 vcpu, 1 GiB memory (Price unavailable)
- Change username to [adminuser].
- Select existing key pair stored in azure.
- Allow ports 80 (http) and 22 (ssh).
- Disks: Standard SSD.
- Select Public subnet.
- Make sure you tick the [Delete public IP and NIC when VM is deleted] box.
- Add tags- Name:Owner, Value:Zainab.
- The vm is the final thing created, all resources are created before it.
### SSH into the VM
- Press the connect button at the top of vm overview.
- Native SSH.
  - Enter the name of the private key in step 3. 
    - Because you're using the name of the private key file, it will only work in the folder where the private key is located.
    - If you want to use a command from any folder, enter the path of the private key instead of name.
    - Command: [ssh -i ~/.ssh/tech501-zainab-az-key adminuser@20.39.218.61].
    - This command can work from any folder. Test it by entering home directory and running command from there. Enter home directory with [cd].
  - Copy the command created right underneath the step.
- Paste command in your git bash terminal. Should connect to the vm. 
- Command: [ssh -i tech501-zainab-az-key adminuser@publicIP]

### Deleting resources
- Go to resource groups.
- Filter out the services by typing "zainab" (naming convention has zainab in all resources)
- Delete all resources except the ssh key and virtual network.

# Linux
- Once inside the vm, run these commands:
  - [sudo apt update -y]
    - Good to use to check if vm is connected to the internet. 
    - Sudo= super user do.
  - [sudo apt upgrade -y]
  
## Bash shell scripting
### Creating a shell script to create an nginx web server.
- [nano provision.sh]
  - Opens an editor and creates the shell file. 
  - Create the script inside this:
    - #update
      sudo apt update -y

      #upgrade
      sudo apt upgrade -y

      #install nginx
      sudo apt install nginx -y

      #restart nginx
      sudo systemctl restart nginx

      #enable nginx - enabled - starts automatically when we start virtual machine.
      sudo systemctl start nginx
      sudo systemctl enable nginx
      #Check if its enable: sudo systemctl is-enabled nginx



- If you make a change to nginx, you need to restart it before those changes are applied.
- systemctl controls system processes e.g. installed tools/services.

## Creating a custom nginx webpage

- To backup the default:
- sudo cp -r /var/www/html /var/www/html_backup

- index.html in the /var/www/html directory
- Enter this in the index.html file [sudo nano index.html]

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



To download the image first:
- sudo wget https://c02.purpledshub.com/uploads/sites/40/2023/08/JI230816Cosmos220-6d9254f-edited-scaled.jpg


Upgraded version with an image link:

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




