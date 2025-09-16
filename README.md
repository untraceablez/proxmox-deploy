# `proxmox-deploy`

This repository is designed to automate the deployment of a Proxmox cluster using Ansible. It includes roles that handle various tasks, such as deploying SSH keys, setting up repositories and packages, networking, and initiating the Proxmox cluster deployment.


## Table of Contents

[Features](#features)

[Prerequisites](#prequisites)

[Installation](#installation)

[Usage](#usage)

[Directory Structure](#directory-structure)

[Roles](#roles)

[Future Plans](#future-plans)

[Contributing](#contributing)


## Features


* SSH Key Deployment: Automates the deployment of SSH keys for secure node communication.

* Repository Setup: Configures necessary repositories for Proxmox and related tools.

* Package Installation: Installs required packages and dependencies.

* Proxmox Cluster Initialization: Sets up and initializes a Proxmox cluster with multiple nodes.


## Prerequisites


* You will need Python3, Python3 pip, and Python3 venv installed. (Install the `python3-full python3-pip` packages with your preferred package manager.)
* You will need a workstation (preferably Linux or WSL) with Ansible installed. (To install Ansible, see the official documentation [here](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).)
* You will need the Ansible Community.general packages as well. (`ansible-galaxy collection install community.general`)
* You will need to install Proxmox on all target nodes, and copy over your Ansible ssh key. This should be done after install using something like `ssh-copy-id`. 



## Installation


1. **Clone the Repository:**

```bash
git clone https://github.com/untraceablez/proxmox-deploy.git
cd proxmox-deploy
```

2. **Create a Python Virtual Environment:**
```bash
mkdir ~/.venv
python3 -m venv ~/.venv/proxmox-deploy
source ~/.venv/proxmox-deploy/bin/activate
```

3. **Install Required Python Packages:**  
```bash
pip install -r requirements.txt
```

4. **Configure Inventory & Ansible Config Files:**  
```bash
cp inventory/hosts_sample.yml inventory/hosts.yml
cp ansible.cfg.sample ansible.cfg
```

## Usage


**Edit Inventory File:**


Modify the inventory.ini file to include your Proxmox nodes. Ensure each node has a unique name and IP address.



**Configure Ansible Config:**

Make sure to update the ansible.cfg file, particularly the `private_key_file` value, which should point to the path of the SSH key you have installed on your nodes.

**Updating Variables:**

Edit the variables in the group_vars/all.yml or host_vars directories for specific configurations.


**Run the Playbook:**


Execute the playbook with the following command:


`ansible-playbook -i inventory.ini main.yml`



Directory Structure

proxmox-deploy/  
├── group_vars/  
│   └── all.yml  
├── host_vars/  
│   └── node1.yml
│   └── node2.yml
│   └── node3.yml
├── inventory/  
│   └── hosts.yml  
├── playbooks/  
│   └── deploy.yml
│   └── update.yml
│   └── deploy-cluster.yml
│   └── deploy-terraform.yml
├── roles/  
│   ├── ssh/  
│   │   ├── tasks/  
│   │   │   └── main.yml  
│   │   └── ...  
│   ├── repositories/  
│   │   ├── tasks/  
│   │   │   └── main.yml  
│   │   └── ...  
│   ├── base/  
│   │   ├── tasks/  
│   │   │   └── main.yml  
│   │   └── ...  
│   ├── cluster/  
│   │   ├── tasks/  
│   │   │   └── main.yml  
│   │   └── ...  
│   ├── sdn/  
│   │   ├── tasks/  
│   │   │   └── main.yml  
│   │   └── ...  
│   ├── networking/  
│   │   ├── tasks/  
│   │   │   └── main.yml  
│   │   └── ...  
│   ├── ceph/  
│   │   ├── tasks/  
│   │   │   └── main.yml  
│   │   └── ...  
│   ├── cloud-init/  
│   │   ├── tasks/  
│   │   │   └── main.yml  
│   │   └── ...  
│   ├── terraform/  
│   │   ├── tasks/  
│   │   │   └── main.yml  
│   │   └── ...  
├── requirements.txt  
├── README.md
├── ansible.cfg  
└── site.yml

## Roles

`base`: This role installs some base packages that are nice-to-haves that I frequently use. Packages that are necessary for the roles to function will be commented as such. Other packages can be added or removed as you see fit.  
`ceph`: This role configures ceph on the cluster. Please note, if you have not configured the cluster yet, this role will only install the ceph packages.   
`cloud-init`: This role configures scripts for cloud-init and downloads your specified cloud-init image for Ubuntu.  
`cluster`: This role initiates the Proxmox cluster and configures the cluster network, migration network, etc.   
`networking`: This role will configure networking on your Proxmox nodes and ensure that all nodes have equivalent *virtual* interfaces. You will need to specify physical to virtual dependencies within the host_vars of each node, *especially* for heterogeneous deployments.
`repositories`: This role configures active repositories on the nodes, disabling the enterprise repos if they're not required, and adding the no-subscription ones in their place.
`sdn`: This role installs the `openvswitch` packages and configures sdn configs on your nodes. It will run the networking role if not already run against the hosts.  
`ssh`: This role configures additional SSH keys beyond Ansible, and hardens SSH configurations.
`terraform`: This role configures Terraform on the nodes, allowing you to manage infrastructure as code. It will run the `cloud-init` role with defaults if it has not been run or configured yet. 

## Future Plans

Not sure yet, but I'm sure I'll think of some things, or I'll get suggestions. 

## Contributing

Contributions are welcome! Please fork the repository, make your changes, and submit a pull request. Ensure you follow the existing coding standards and provide clear documentation for any new roles or features added. Feel free to reach out if you have any questions or need further assistance with setting up your Proxmox cluster using Ansible.

