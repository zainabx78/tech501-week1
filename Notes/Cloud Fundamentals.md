# CLOUD INTRO

- Centrally managed.
- Service available over the internet.
- **IAAS**- Your responsibility is OS, middleware, runtime, applications and data.
- **PaaS**- Your responsibility is applications and data.
- **SaaS**- Data. 

#  AZURE CLOUD
### Good practices:

- Naming conventions- Add the actual resource name at the end of the name. E.g If you're creating a vnet, name it **tech501-zainab-test-vnet**.
- Tags- Name:Owner and Value:Zainab.

Virtual machines live in virtual networks (vnets). Also require subnets. 

Public Ip addresses cost money. They're also optional. Private IP addresses are allocated to the VM's from the subnet CIDR block. 


## To create a keypair:

- ~ = home directory. 
.ssh folder needs to exist in that. 

- Any file or folder starting with [.] is hidden. 

- To view hidden files/folders: [ls -a].
- change directories to be in the .ssh folder to create the keypair in. [cd .ssh]

- [ssh-keygen -t rsa -b 4096 -C "zainabfarooq001@gmail.com"]
  
- The public key generated will be put onto azure to use for the VM. 
- The private key will be used when you want to access the vm. 