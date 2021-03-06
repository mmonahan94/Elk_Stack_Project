# Elk_Stack_Project
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text](https://github.com/mmonahan94/Elk_Server_Project/blob/a538e15d6cdf4ca56f742f38e24869bbbecbd21d/Images/Elk-Server-Diagram.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yaml file may be used to install only certain pieces of it, such as Filebeat.

[elk_config.yml](https://github.com/mmonahan94/Elk_Server_Project/blob/a29f02ce24227afd364d6dd5c65e54db0b748397/Ansible/elk_config.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure, in addition to restricting traffic to the network.
-: Load balancers protects the organization from potential DDoS attacks by limiting traffic to the network. A jump box is a secure device that all admins first connect to before launching any administrative task or use as an origination point to connect to other servers or untrusted environments.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the metrics and system logs.
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing
- Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name     | Function | IP Address               | Operating System |
|----------|----------|--------------------------|------------------|
| Jump Box | Gateway  | 10.0.0.4                 | Linux            |
| Web-1    |    VM    | 10.0.0.8                 | Linux            |
| Web-2    |    VM    | 10.0.0.9                 | Linux            |
| Web-x    |    Elk   | 10.1.0.4, 20.122.71.79   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the host machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 98.204.108.168
- 20.106.140.255
- 20.122.71.79
	
Only the JumpBoxProvisioner machine can accept connections from the Internet. 

A summary of the access policies in place can be found in the table below.

|    Name     |    Publicly Accessible    | Allowed IP Addresses  |
|-------------|-------------------------- |-----------------------|
| Jump Box    |      Yes                  | Personal IP           |
| Web-1       |      No                   | 10.0.0.4, 10.0.0.9    |
| Web-2       |      No                   | 10.0.0.4, 10.0.0.8    |
| Web-X       |      Yes                  | 10.0.0.4, Kibana      |
| Red-Team-LB |      Yes                  | Personal IP           |



### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because one can create a code that can be used multiple times for various configurations. 


The playbook implements the following tasks:
- Install Docker
- Install pip3
- Install Docker Python Module
- Increate virtual memory
- Downloand and launch a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![alt text](https://github.com/mmonahan94/Elk_Server_Project/blob/5fa76ab8366dd4ef2d940553cc12c6d5d2e824be/Images/Docker_PS.JPG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.8
- Web-2: 10.0.0.9

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat allows for a lightweight way to forward and centralize logs and files. This provides a GUI and infographic view in order to track down curious behavior across aggregated logs.
- Metricbeat allows for a lightweight way to send system and service statistics. This provides a GUI and infographic view of system-level CPU usage, memory, file system, disk IO, network IO statistics, and top-like statistics for every process running on your systems.

### Evidence of Success
Below are screenshots captured from successful installations of both Filebeat and Metricbeat:

### Successful Filebeat Installation
![alt text](https://github.com/mmonahan94/Elk_Server_Project/blob/e50fe5a0cfe174adac8e601516779b2730d7f86c/Images/Filebeat_Success.JPG)

### Successful Metricbeat Installation 
![alt text](https://github.com/mmonahan94/Elk_Server_Project/blob/e50fe5a0cfe174adac8e601516779b2730d7f86c/Images/Metricbeat_Success.JPG)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the entire Ansible folder to /etc/ansible/<Designated Name>
- Update the host file to include the IP addresses for your webservers and your elkserver
- Update each Config file appropriately to your designated machines.
- Run the playbooks, and navigate to http://<Elk-Server-Public-IP>:5601 to check that the installation worked as expected.

Answer the following questions to fill in the blanks:_
- There are 2 playbooks. Once called filebeat_playbook.yml and the other metricbeat_playbook.yml. You should copy these to ~/etc/ansible/filebeat and ~/etc/ansible/metricbeat , respectfully.
- There is a host file you need to update to specify which machine to install the elk server on.  Specifying the host group at the beginning of the playbook file determines the machines you install the ELK server and/or Fillebeat on
- To check if the Elk server is working go to 'http://<Web-x Public IP Address>:5601/app/kibana'. If the page loads successfully then you know it is working. 
