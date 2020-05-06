
# Install Packer: #
* Install Packer first, it is available for different OS's and can be downloaded on https://packer.io/downloads.html (This installation has been tested with the Linux and Mac version)


# Preparation: #
Adjust the required variables in the ubuntu1804.json file
    
Go to the section called variables, and adjust the necessary variables, such as the vcenter connection data and datastore

# Installatie Kube master #

Open a Terminal or DOS/Powershell prompt and go to the cloned ubuntu directory

    
Perform the following command ``` "packer build -var vm-name=kube-master ubuntu1804.json" ``` (where the vm name is a variable value, this will be the VM and host name)

After it is finished Turn on the Kube-Master VM and continue


# Installatie Kube Nodes #

Open a Terminal or DOS/Powershell prompt and go to the cloned ubuntu directory

    
** Run the following command ``` "packer build -var vm-name=kube-node1 ubuntu1804.json" ``` (where the vm name is a variable value, this will be the VM and host name)

** Repeat the above step for each node you want to add, make sure that the subsequent vm-name contains the term node. (so kube-node2 etc)

# After installation #

* During installation, a user with username Ubuntu is created. A public key is also installed. The private key (id_) is located in the packer_kubernetes/sshkey directory. A passwordless ssh connection can now be set up. (use "ssh -i sshkey/id_k8s ubuntu@kube-master-ip" for the ssh connection, to use the private key)
* Make a ssh connection to the kube-master node. You can now get under the user ubuntu with kubectl to get started.

# Possible error messages: #

Booting the VM failed -> Controleer de connectie naar de vCenter

# Advanced settings: #

The default password for the ubuntu user is Password!01, it can be changed the installation.

# Reassemble Cluster #

* Remove the sshkey keys from the packer_kubernetes/sshkey directory.
* Remove the print-joincommand.sh script from the packer_kubernetes/join-command directory.
* Remove the VMs
* Follow the steps above again

## License

MIT / BSD


