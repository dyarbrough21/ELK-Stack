# ELK-Stack
Creation of a Virtual Network and additional components
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

  - https://github.com/dyarbrough21/ELK-Stack/blob/main/ELK-Stack/Ansible/DVWAInstall.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant and resilient, in addition to restricting access to the network.
Load balancers allow for availability of a network, ensuring that the load is spread across all of the Web VMs so that if one becomes unavailable, the others will still be accessible.  

The jump box restricts access to the other VMs on the network from external networks and requires SSH access into each box individually only from the jump box.  The jump box is the only entry point into the Web VMs and protects the data from outside the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system files.  

Filebeat forwards and centralizes log data. Filebeat is installed on the servers and monitors the log files, collects log events, which are visually displayed in the Kibana interface.  

Metricbeat collects metrics from the system and services and is a lightweight way to send system and service statistics, which are visually displayed in the Kibana interface.

The configuration details of each machine may be found below.

| Name        | Function   | Local IP Address | Operating System |
|-------------|------------|------------------|------------------|
| Jump Box    | Gateway    | 10.4.0.4         | Linux            |
| Web1-Offsec | Webserver  | 10.4.0.5         | Linux            |
| Web2-Offsec | Webserver  | 10.4.0.6         | Linux            |
| Web3-Offsec | Webserver  | 10.4.0.7         | Linux            |
| Elk Server  | Monitoring | 10.1.0.4         | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 73.137.170.67

The Firewall rules need to be changed to allow traffic from only my Public IP address listed above.

Machines within the network can only be accessed by the Jump Box local IP address:
10.4.0.4


A summary of the access policies in place can be found in the table below.
| Name          | Publicly Accessible | Allowed IP Addresses    |
|---------------|---------------------|-------------------------|
| Jump Box      | Yes                 | 73.137.170.67           |
| Web1-Offsec   | No                  | 10.4.0.4                |
| Web2-Offsec   | No                  | 10.4.0.4                |
| Web3-Offsec   | No                  | 10.4.0.4                |
| Elk Server    | Yes                 | 10.4.0.4, 73.137.170.67 |
| Load Balancer | Yes                 | 73.137.170.67           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because Ansible is able to manage more than one machine at a time as well as reduce human error and save time.  It makes automating tasks easy using YAML via Ansible Playbooks to carry out actions.  

The playbook implements the following tasks:

Installs Docker.io
Uninstalls Apache2
Install pip3
Installs Docker Module
Downloads and launches the docker web container
Enables docker to start on every machine boot up

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
The Virtual Machines with internal IP addresses 10.4.0.5, 10.4.0.6 and 10.4.0.7

We have installed the following Beats on these machines:
Both Filebeat and Metricbeat have been installed on each machine.

These Beats allow us to collect the following information from each machine:
Filebeat collects system log data.  We can track the hostnames and processes being run on each host system. 
Metricbeat collects docker container metrics.  We can track CPU usage, Memory usage and Network Input/Output to see time attributed to sending data between monitored processes.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

Run the playbooks, DVWA, ELK, Filebeat and Metricbeat from the /etc/ansible/roles directory.   Update the /etc/ansible/hosts file to include the IP address in the webservers and ELK.  Uncomment the webservers and ensure that the virtual machine private IP addresses are listed.  Run the playbook and navigate to ELKPublicIP:5601/app/kibana#/home to check that the installation worked as expected.


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
