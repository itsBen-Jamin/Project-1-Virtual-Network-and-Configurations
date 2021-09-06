# Project-1-Virtual-Network-with-ELK-Stack-Deployment-and-Configurations
The files in this repository were used to configure the network depicted below.
![Cloud Security Diagram](https://user-images.githubusercontent.com/79231152/131538631-c770ecc4-6acb-442a-b129-e230426a4ee8.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

![filebeat-playbook.yml](https://github.com/itsBen-Jamin/Project-1-Virtual-Network-and-Configurations/files/7085395/filebeat-playbook.yml.txt) [Select this file to Download .txt copy of filebeat-playbook | to view select the file in the README repository above]

![metricbeat-playbook.yml](https://github.com/itsBen-Jamin/Project-1-Virtual-Network-and-Configurations/files/7085661/metricbeat-playbook.yml.txt) [Select this file to Download .txt copy of metricbeat-playbook | to view select the file in the README repository above]


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application and/or web site will be highly available by evenly distributing traffic to diferent a server(s), in addition to restricting unintended guests directly into the network.
- _Load Balancers provide a few different levels of security. For example, the main intended use of a load balancer, is to assist a website that is receives high volumes of web traffic. The load balancer will decide when one server is being overloaded by the traffic and will then redirect the traffic to another server within the same container, offloading the full stress, from the priority server. Which could result in Denial of Service(DoS). They recieve daily rule updates just like a virus scanner and the Load Balancer is also given it's own public IP. Having it's own Public IP, backed by a Jump Box, will make sure that the only traffic coming threw it are HTTP request. Making the web servers only accessable from a Jump Box. A Jump Boxes biggest advantages is allowing a one way connection with a server threw a SSH key, uniquely identified to a specific remote machine_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the traffic and system logs.
- _Filebeat is a program that assists in collection, generation, and the organization of log events pertaining to a specified server, including this ELK server. Specifically, Filebeat monitors any actions and changes within the system and marks them with a timestamp_
- _Metricbeat is assists in monitoring and makeing changes to a system that doesnt have Graphical User Inerface(GUI). Using Metricbeat you can monitor any processes running on that system that may be drawing from the systems resources_

The configuration details of each machine may be found below.
| Name          | Function          | IP Address   | OS    |
|---------------|-------------------|--------------|-------|
| Jump Box      | Gateway           | 10.0.0.4     | Linux |
| Web-1         | DVWA              | 10.0.0.5     | Linux |
| Web-2         | DVWA              | 10.0.0.6     | Linux |
| Web-3         | DVWA              | 10.0.0.7     | Linux |
| Load Balancer | Balancing Traffic | 20.106.134.5 | N/A   |
| ELK-Server    | File/Metricbeat   | 13.64.108.55 | Linux |

### Access Policies

The Web machines on the internal network are not exposed to the public Internet. 

Only the Load Balancer machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _My private home IP address or any additional whitelisted IP address that need to be added_

Machines within the network can only be accessed by the Ansible Jump Box.
- _Ansible Jump Box: IP@ 13.68.235.99_

A summary of the access policies in place can be found in the table below.
| Name          | Publicly Accessible | Allowed IP Address |
|---------------|---------------------|--------------------|
| Jump Box      | No ONLY via SSH     | My Private IP      |
| Web-1         | No                  | 10.0.0.4           |
| Web-2         | No                  | 10.0.0.4           |
| Web-3         | No                  | 10.0.0.4           |
| Load Balancer | Yes                 | WAN                |
| ELK-Server    | No                  | 10.0.0.4           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _In the case of events that a web server is compromised, Ansible makes destroying and redeploying those servers more convenient by deploying these same automations without fail_

The playbook implements the following tasks:
- _Installs Docker_
- _Installs Python 3_
- _Installs Docker pip Module_
- _Increases Virtual Memory_
- _Downloads and Launches Docker ELK container_
- _Creates Docker Images_

[ELKplaybook.yml](https://github.com/itsBen-Jamin/Project-1-Virtual-Network-and-Configurations/files/7086464/ELKplaybook.yml.txt)


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img width="949" alt="Capture69" src="https://user-images.githubusercontent.com/79231152/131570554-c6275f51-8153-4d3d-94e2-c68885def872.PNG">

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _Web-1 @ 10.0.0.5_
- _Web-2 @ 10.0.0.6_
- _Web-3 @ 10.0.0.7_

We have installed the following Beats on these machines:
- _Filebeat_
- _Metricbeat_

These Beats allow us to collect the following information from each machine:
- _Filebeat collects and generates logs displaying system audits. Audit logs collect data documenting resources that were accessed, also including the destination and source addresses, timestamps, and user login information correlating to those addresses for later examination_
- _Metricbeat collects statistics relating to the health of the system. Logging data such as CPU, memory, data, and resource usage._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below: (Similar steps also apply to the Metricbeat-Playbook)
- _Copy the /etc/ansible/filebeat-config.yml file to /etc/filebeat/filebeat.yml._
- _Update the filebeat-config.yml file to include the control node's IP address._
- _Run the playbook, and navigate to Jump Box machine to check that the installation worked as expected._


### Steps not specified:

- _Playbooks are located in the /etc/ansible file_
- _Remote machine will need to be specified in the ansible.cfg._
- _To specifing what machine to direct a YAML files to, you will need to set the desired 'host(s)' as the target inside desired YAML file_
- _To make sure the ELK server is recieving logs navigate to http://13.64.108.55:5601/app/kibana#/home and make sure Kibana is collecting data from the ELK stack_

### Red-Team NSG Rules and Reason

| Priority 	| Name            	| Port 	| Protocol 	| Source       	| Destination 	| Action 	|
|----------	|-----------------	|------	|----------	|--------------	|-------------	|--------	|
| 500      	| Allow_RDP       	| 3389 	| TCP      	| MY PRIV. IP  	| VNet        	| Deny   	|
| 4090     	| Allow_SSH_2_ELK 	| 5601 	| TCP      	| 13.68.235.99 	| 10.1.0.4    	| Allow  	|
| 4093     	| Allow_HTTP_VNet 	| 80   	| TCP      	| MY PRIV. IP  	| VNet        	| Allow  	|
| 4094     	| Allow_SSH_VNet  	| 22   	| TCP      	| MY PRIV. IP  	| VNet        	| Allow  	|
| 4095     	| Allow_SSH       	| 22   	| TCP      	| MY PRIV. IP  	| 10.0.0.4    	| Allow  	|

_Rule #1: Allow_RDP_-   RDP(Remote Desktop Protocol) has a predefined port number of 3389. This rules allows for Remote Desktop Protocol from only my specified IP address if the action was decided to be Allowed with a high priority of 500.

_Rule #2: Allow_SSH_2_ELK_-   This rule runs on specified port 5601 for the ELK server. This rule was placed to allow for the Ansible Jump Box access.

_Rule #3: Allow_HTTP_VNet_-   Threw port 80, this rule allows me only (or if left open, anyone with the known web server's IP address) to send HTTP requests to the Red-Team's virtual network Web servers

_Rule #4: Allow_SSH_VNet_-  SSH is predefined on port 22 and this rule is is place to allow ONLY my IP access to the VNet for security reasons. This specifacally grant only one user to be able to access the back-end of the web servers threw a jump box realating to my IP and machine's generated SSH Key

_Rule #5: Allow_SSH_- Like the last rule, this one is in place to for the security reason of only allowing my IP to be allowed to access the Jump Box. This rule is set with the lowest prioritiy because it will be the first action taken to access both the Red-Team VNet and RedELK VNet. Haviong this rule any higher than the others would result rule conflicting


### RedELK NSG Rules and Reasons

| Priority 	| Name                 	| Port 	| Protocol 	| Source        	| Destionation 	| Action 	|
|----------	|----------------------	|------	|----------	|---------------	|--------------	|--------	|
| 500      	| Allow_ELKrdp         	| 3389 	| TCP      	| MY PRIV. IP   	| 13.64.108.55 	| Deny   	|
| 4090     	| Allow_SSH_frm_Home   	| 5601 	| TCP      	| MY PRIV. IP   	| VNet         	| Allow  	|
| 4095     	| Allow_SSH_FRM_Jump   	| 22   	| TCP      	| 40.121.145.59 	| 10.1.0.4     	| Allow  	|

_Rule #1: Allow_ELKrdp_-  This rule has a high priority for reasons of instant start up on if the action is Allowed. This would only be accesable threw my private IP or any other whitelisted IP needed. This rule was added just as an example. This ELK server doe not have any GUI other than the Kibana Sites GUI

_Rule #2: Allow_SSH_frm_Home_- To keep the ELK stack secure, threw only port 5601 can my private IP access the ELK stack's Virtual Network.

_Rule #3: ALLow _SSH_FRM_Jump_- For security reasons as well, this rule allows only the Jump Box IP to access the information being sent to the ELK Server. Via the remote location on that Jump Box threw SSH
