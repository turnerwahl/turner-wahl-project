# turner-wahl-project
Azure network and security info


## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Cloud Diagram](Diagrams/Cloud_Diagram.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

[ELK Setup Playbook](Ansible/Elk_Playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the web traffic and system metrics.


The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name                 | Function   | IP Address | Operating System |
|----------------------|------------|------------|------------------|
| Jump-Box-Provisioner | Gateway    | 10.0.0.4   | Linux            |
| Web-1                | Web Server | 10.0.0.5   | Linux            |
| Web-2                | Web Server | 10.0.0.6   | Linux            |
| Web-3                | Web Server | 10.0.0.8   | Linux            |
| ELK-VM               | Monitoring | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine and ELK machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
75.168.76.102

Machines within the network can only be accessed by SSH from the Jump Box machine, on IP 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses   |
|----------------------|---------------------|------------------------|
| Jump-Box-Provisioner | Yes                 | 75.168.76.102          |
| Web-1                | No                  | 10.0.0.4               |
| Web-2                | No                  | 10.0.0.4               |
| Web-3                | No                  | 10.0.0.4               |
| ELK-VM               | Yes                 | 75.168.76.102 10.0.0.4 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because the process is automated, consistent, and easy to replicate.

The playbook implements the following tasks:
- Installs docker and python3 package utilities
- Configures the vm to allow greater memory use
- Download and configure the ELK docker container
- Enable docker service on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Diagrams/Docker_PS.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
10.0.0.5 - Web-1
10.0.0.6 - Web-2
10.0.0.8 - Web-3

We have installed the following Beats on these machines:
FileBeats
MetricBeats

These Beats allow us to collect the following information from each machine:
Filebeats monitors system logs, including sudo command usage. MetricBeats monitors system metrics, including CPU usage, Memory usage, and disk usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Elk_Playbook.yml file to /etc/ansible/
- Update the hosts file to include the 'elk' hosts group and 'webservers' hosts group and the corresponding IP addresses and the python interpreter.
- Run the playbook, and navigate to 20.98.152.182:5601/app/kibana to check that the installation worked as expected.


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

Download the filebeat configuration file with the following command:
curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat >> /etc/ansible/files/filebeat-config.yml
Edit lines 1106 and 1806 for the correct IP addresses.

Download the Elk_Playbook.yml using the following command:
curl https://github.com/turnerwahl/turner-wahl-project/Ansible/Elk_Playbook.yml >> /etc/ansible/Elk_Playbook.yml

Run the playbook with the following command:
ansible-playbook /etc/ansible/Elk_Playbook.yml