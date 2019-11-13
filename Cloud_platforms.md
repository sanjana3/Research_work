# Microsoft Azure VM setup 

Azure virtual machines can be created through the Azure portal. The Azure portal is a browser-based user interface to create Azure   resources. This quickstart shows you how to use the Azure portal to deploy a Linux virtual machine running Ubuntu 18.04 LTS. 
 
* If you don't have an Azure subscription, create a free account before you begin.
### STEP1 : Create SSH key pair 

* You need an SSH key pair to complete this quickstart. If you already have an SSH key pair, you can skip this step. Open a bash shell and use ssh-keygen to create an SSH key pair. If you don't have a bash shell on your local computer, you can use the Azure Cloud Shell.
* Sign in to the Azure portal. In the menu at the top of the page, select the ```>_``` icon to open Cloud Shell. Make sure the CloudShell says Bash in the upper left. If it says PowerShell, use the drop-down to select Bash and select Confirm to change to the Bash shell.
* Type ```ssh-keygen -t rsa -b 2048``` to create the ssh key.You will be prompted to enter a file in which to save the key pair. Just press Enter to save in the default location, listed in brackets.You will be asked to enter a passphrase. You can type a passphrase for your SSH key or press Enter to continue without a passphrase.
The ```ssh-keygen``` command generates public and private keys with the default name of id_rsa in the ```~/.ssh``` directory. The command returns the full path to the public key. Use the path to the public key to display its contents with cat by typing ```cat ~/.ssh/id_rsa.pub```. 
* Copy the output of this command and save it somewhere to use later in this article. This is your public key and you will need it when configuring your administrator account to log in to your VM.

### STEP2 : Create a virtual machine

1. Sign in to Azure portal
2. Choose **Create a resource** in the upper left corner of the Azure portal. In **Popular**, select **Ubuntu Server 18.04 LTS**.
3. In the **Basics** tab, under **Project details**, make sure the correct subscription is selected and then choose to **Create new** under **Resource group**. Type *myResourceGroup* for the name of the resource group and then choose **OK**.
![1](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/media/quick-create-portal/project-details.png)
4. Under Instance details, type *myVM* for the Virtual machine name and choose East US for your Region. Leave the other defaults.
![2](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/media/quick-create-portal/instance-details.png)
5. Under **Administrator account**, select SSH public key, type your user name, then paste in your public key. Remove any leading or trailing white space in your public key.
![3](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/media/quick-create-portal/administrator-account.png)
6. Under **Inbound port rules > Public inbound ports**, choose Allow selected ports and then select SSH (22) and HTTP (80) from the drop-down.
![4](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/media/quick-create-portal/inbound-port-rules.png)
7. Leave the remaining defaults and then select the **Review + create** button at the bottom of the page.

8. On the Create a virtual machine page, you can see the details about the VM you are about to create. When you are ready, select Create. It will take a few minutes for your VM to be deployed. 

### STEP3 : Connect to the Virtual Machine

1. Select the **Connect** button on the overview page for your VM.
![5](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/media/quick-create-portal/portal-quick-start-9.png)
2. In the Connect to virtual machine page, keep the default options to connect by IP address over port 22. In Login using VM local account a connection command is shown. Select the button to copy the command. The following example shows what the SSH connection command looks like:    ```ssh username@IP address ``` i.e. ```ssh azureuser@10.111.12.123```
3. Using the same bash shell you used to create your SSH key pair (you can reopen the Cloud Shell by selecting >_ again, paste the SSH connection command into the shell to create an SSH session.

### STEP4 : Opening a port for jupyter

1. After the virtual machine deploys we need to open up a security rule on the network security group. From the Azure portal, go to Network Security Groups and open the tab for the Security Group corresponding to your VM. You need to add an Inbound Security rule with the following settings: TCP for the protocol, * for the source (public) port and 9999 for the destination (private) port.

![6](https://github.com/rgl/azure-content/raw/master/articles/virtual-machines/media/virtual-machines-linux-jupyter-notebook/azure-add-endpoint.png)
2. While in your Network Security Group, click on Network Interfaces and note the Public IP Address as it will be needed to connect to your VM in the next step.
#### Installing Anaconda3 2.3.0 64-bit on Ubuntu for jupyter
``` # Installing anaconda
    pwd 
    mkdir -p anaconda
    cd anaconda/
    curl -O https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh
    bash Anaconda3-5.0.1-Linux-x86_64.sh
    
    # To activate the installation
    source ~/.bashrc
    conda list
    
    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter to the latest install and generate its config file
    sudo anaconda3/bin/conda install jupyter -y
    anaconda3/bin/jupyter-notebook --generate-config
``` 
![7](https://github.com/rgl/azure-content/raw/master/articles/virtual-machines/media/virtual-machines-linux-jupyter-notebook/anaconda-install.png)

#### Configuring Jupyter and using SSL
``` cd ~/.jupyter
    
    # To create SSL certificate(Linux & Windows)
    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem
    
    # To set a password protecting
    anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"
    
    # To run jupyter
    anaconda3/bin/jupyter-notebook
    
```



Helpful links:
* https://github.com/rgl/azure-content/blob/master/articles/virtual-machines/virtual-machines-linux-jupyter-notebook.md
* https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal?toc=%2Fazure%2Fvirtual-machines%2Flinux%2Ftoc.json
* https://www.digitalocean.com/community/tutorials/how-to-install-the-anaconda-python-distribution-on-ubuntu-16-04

