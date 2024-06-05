# IP 3 Configuration Management (Ansible, Vagrant)

This is a set up for an automated Ansible configuration playbook that automates configurations on a Vagrant provisioned server.

### Requirements
- Ansible Installed
- Vagrant Installed
- VirtualBox Installed


## How to run
To run the configurations, go through these steps:

Use `vagrant up`command to create and provision virtual machines as defined in the Vagrantfile. 
- When you run the command, Vagrant reads the configuration from the Vagrantfile and starts the virtual machine according to the specified settings.

Use `vagrant provision` command to run the provisioning process on an already running Vagrant virtual machine.
- The command is used to update and reapply provisioning to an already running Vagrant virtual machine without having to recreate it from scratch.

### Other Commands
`vagrant status` 
 command is used to check the current status of Vagrant-managed virtual machines in the current Vagrant environment.

`vagrant halt` 
command is used to shut down Vagrant-managed virtual machines.

- ![Screenshot from 2024-06-05 14-06-31](https://github.com/Jmaisiba/yolo/assets/35705417/4ac9c267-3927-4321-a32d-8b0bce552504)


 `vagrant ssh`
 command is used to SSH into vagrant managed virtual machines

 - ![Screenshot from 2024-06-05 13-52-54](https://github.com/Jmaisiba/yolo/assets/35705417/0aef1e7f-aa94-41c8-8383-8938087410bc)


## What you should expect
### Running vagrant up
When you run the `vagrant up` command the following output should be expected signalling start of virtual machine

- ![Screenshot from 2024-06-05 13-45-22](https://github.com/Jmaisiba/yolo/assets/35705417/28e7f544-d679-4b36-b049-d73972bc75ea)

### Running vagrant provision
Running `vagrant provision` carries out tasks/roles assigned in playbook. 
This is a snippet of final tasks being complete with high verbosity(this can be changed)
You also get a summarry of tasks carried out and the state

- ![image](https://github.com/Jmaisiba/yolo/assets/35705417/57e99870-ed6a-4bd4-8096-4cfd5e35011e)


### Expected outcome
Ater SSH into the virtual machine using`vagrant ssh` you can run `docker ps` to check the running containers in the virtual machine
As from the image we can see our tasks carried out by the roles have been satisfied all from the `vagrant provision` command

- ![Screenshot from 2024-06-05 13-56-52](https://github.com/Jmaisiba/yolo/assets/35705417/61e23c07-e59a-4e19-825a-1090e113258c)




## What makes these Configurations Possible?

## Vagrant File

`vagrant init` command automatically initializes a new vagrant environment and generates a Vagrantfile in the directory

This is a configuration file used by Vagrant for building and managing virtual machine environments. 
The file defines and automates the setup of development environments in a consistent and reproducible manner.  
It simplifies the process of creating and managing virtual machines, ensuring consistency across different development environments.

### Vagranfile content
Content of the file serves as the configuration for the Vagrant environment, specifying settings such as the base box, network configuration, and provisioning options.
However, one has to add some content to the Vagrantfile for it to be usable through ansible

`config.ssh.insert_key = false` 
This disables the insertion of SSH keys into the VM

`config.vm.provision "ansible" do |ansible|`
This configures Vagrant to provision the virtual machine using Ansible

`ansible.verbose = "vv"`
This defines amount of details in the logs

`ansible.playbook = "playbook.yaml"`
This specifies the playbook file vagrant is to use

## Ansible Config File
This file sets the configurations amd path to where Ansible is to check for target host

### ansible.cfg contents
`[defaults]:` 
Indicates that configuration applies to the default settings of Ansible as they come by default.

`inventory = hosts:` 
Specifies the inventory file to be used by default when running Ansible commands. In this case, it sets the inventory file to hosts which is in the current directory.

## Ansible Inventory File

The Ansible inventory file defines the hosts and their connection settings.

### Inventory File Contents

`yolo-ip3-server:` 
This is the name/alias tha represents the hostname of the target host in the inventory. It's the name by which Ansible recognizes the host.

`ansible_connection=local:` 
This is the connection method to the target host. In this case, local indicates that Ansible should run tasks locally on the control node.

## Ansible Playbook

The Ansible playbook automates various tasks related to setting up and configuring Docker environments on a VM host and running the associated containers.

### Playbook Content Explanation:
`hosts: all`
Specifies it targets all the hosts for the tasks to be executed. 
Ansible will connect to each host specified in the hosts config file and execute the tasks defined in the playbook.
  
`become: true`
This is privilege escalation, allowing the tasks to be executed with elevated privileges similar to using `sudo`. 
This is required for some of the tasks that involve system configurations or installations.


`roles:`
This list of Ansible roles to be applied to the hosts. 
Each role represents a set of tasks and configurations related to a specific aspect of setting up Docker environments. 

### Breakdown of the roles:

`VM-connection-testing`
This tests the connection to the remote VM using the `ping` command
      
`git-repository-cloning`
Clones Git repositoriy containing Docker configurations or application code.

`ubuntu-apt-library-updates`
Update the Ubuntu APT package library to ensure the latest package information is available.

`docker-installation-prep`
Prepare the system for Docker installation by ensuring necessary dependencies are installed and configuring package repositories.

`docker-install`
Install Docker engine on the target hosts.

`docker-environment`
Configure Docker environment settings such adding vagrant(current user) to docker user group.

`docker-compose-installation`
Install Docker Compose, a tool for defining and running multi-container Docker applications.

`docker-compose-deployment`
Handle the deployment of Docker Compose configurations and managing Dockerized applications.
