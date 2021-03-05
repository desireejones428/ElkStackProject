## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

	ElkStackProject/Diagrams/DAJ-ELKStackNetworkDiagram.drawio
	https://github.com/desireejones428/ElkStackProject/blob/main/Diagrams/DAJ-ELKStackNetworkDiagram.drawio

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

	ElkStackProject/Scripts
	https://github.com/desireejones428/ElkStackProject/tree/main/Scripts

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
- Load balancers will balance the load of the internet-facing web servers. The advantage of a jump box is to control the access of the incoming traffic.  


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMs on the network and system metrics.
- CPU usage and SSH attemps are examples of system metrics

The configuration details of each machine may be found below.


| Name               | Function   | IP Address | Operating System |
|--------------------|------------|------------|------------------|
| JumpBoxProvisioner | Gateway    | 10.0.0.4   | Linux            |
| Web-1              | Web Server | 10.0.0.5   | Linux            |
| Web-2              | Web Server | 10.0.0.6   | Linux            |
| DVWA-Web3          | Web Server | 10.0.0.7   | Linux            |
| ELK-SERVER         | Monitoring | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 24.23.65.101 (my public IP address)

Machines within the network can only be accessed by each other.
- Web-1, Web-2 and DVWA-Web3 are able to send traffic to the ELK Server.

A summary of the access policies in place can be found in the table below.

| Name               | Publicly Accessible | Allowed IP Addresses                |
|--------------------|---------------------|-------------------------------------|
| JumpBoxProvisioner | Yes                 | 24.23.65.101 [My Public IP address] |
| Web-1              | No                  | 10.0.0.1-254 10.1.0.1-254           |
| Web-2              | No                  | 10.0.0.1-254 10.1.0.1-254           |
| DVWA-Web3          | No                  | 10.0.0.1-254 10.1.0.1-254           |
| ELK-SERVER         | No                  | 10.0.0.1-254 10.1.0.1-254           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it speeds up the process. It also ensures consistency across multiple deployments.

The playbook implements the following tasks:
- Install Docker
- Install Python3
- Expands the memory of the virtual machine
- Downloads and launches a docker elk container
- Enables the service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

ElkStackProject/Scripts/Images/DockerPS.png


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5 Web-1
- 10.0.0.6 Web-2
- 10.0.0.7 DVWA-Web3

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors the filesystem and detects any changes.
- Metricbeat monitors the system metrics and detects any changes (i.e. CPU usage).

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbooks file to Ansible control node.
- Update the hosts file to include the hosts for the [webservers] and the host for the [elk] server.
- Run the playbook, and navigate to http://104.42.196.199:5601 or http://[elk_public_IP]:5601 to check that the installation worked as expected.
