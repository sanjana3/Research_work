# Cloud Platforms

# Microsoft Azure

ssh sanjana@104.211.55.56
104.211.55.56

https://repo.continuum.io/archive/Anaconda3-5.2.0-Linux-x86_64.sh

* Create a linux virtual machine using Azure portal

 Azure virtual machines (VMs) can be created through the Azure portal. The Azure portal is a browser-based user interface to create Azure   resources. This quickstart shows you how to use the Azure portal to deploy a Linux virtual machine (VM) running Ubuntu 18.04 LTS. To see your VM in action, you also SSH to the VM and install the NGINX web server.
 
* If you don't have an Azure subscription, create a free account before you begin.
### Create SSH key pair 
* You need an SSH key pair to complete this quickstart. If you already have an SSH key pair, you can skip this step. Open a bash shell and use ssh-keygen to create an SSH key pair. If you don't have a bash shell on your local computer, you can use the Azure Cloud Shell.
* Sign in to the Azure portal. In the menu at the top of the page, select the ```>_``` icon to open Cloud Shell. Make sure the CloudShell says Bash in the upper left. If it says PowerShell, use the drop-down to select Bash and select Confirm to change to the Bash shell.
* Type ```ssh-keygen -t rsa -b 2048``` to create the ssh key.You will be prompted to enter a file in which to save the key pair. Just press Enter to save in the default location, listed in brackets.You will be asked to enter a passphrase. You can type a passphrase for your SSH key or press Enter to continue without a passphrase.
The ```ssh-keygen``` command generates public and private keys with the default name of id_rsa in the ```~/.ssh``` directory. The command returns the full path to the public key. Use the path to the public key to display its contents with cat by typing ```cat ~/.ssh/id_rsa.pub```. Copy the output of this command and save it somewhere to use later in this article. This is your public key and you will need it when configuring your administrator account to log in to your VM.

### Create virtual machine
1. Sign in to Azure portal
2. Choose **Create a resource** in the upper left corner of the Azure portal. In **Popular**, select **Ubuntu Server 18.04 LTS**.
3. In the **Basics** tab, under **Project details**, make sure the correct subscription is selected and then choose to **Create new** under **Resource group**. Type *myResourceGroup* for the name of the resource group and then choose **OK**.
![1](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/media/quick-create-portal/project-details.png)
4.Under Instance details, type myVM for the Virtual machine name and choose East US for your Region. Leave the other defaults.

5.Under Administrator account, select SSH public key, type your user name, then paste in your public key. Remove any leading or trailing white space in your public key.

6.Under Inbound port rules > Public inbound ports, choose Allow selected ports and then select SSH (22) and HTTP (80) from the drop-down.

7.Leave the remaining defaults and then select the Review + create button at the bottom of the page.

8. On the Create a virtual machine page, you can see the details about the VM you are about to create. When you are ready, select Create.

It will take a few minutes for your VM to be deployed. 




# Google Cloud Platform
a.	Google Collab is similar as Azure Notebooks
# Amazon Web Services
