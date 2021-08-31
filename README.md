# Project-1-Virtual-Network-with-ELK-Stack-Deployment-and-Configurations
The files in this repository were used to configure the network depicted below.
![Cloud Security Diagram](https://user-images.githubusercontent.com/79231152/131538631-c770ecc4-6acb-442a-b129-e230426a4ee8.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

[filebeat-playbook.yml](https://github.com/itsBen-Jamin/Project-1-Virtual-Network-and-Configurations/files/7085395/filebeat-playbook.yml.txt)

[metricbeat-playbook.yml](https://github.com/itsBen-Jamin/Project-1-Virtual-Network-and-Configurations/files/7085661/metricbeat-playbook.yml.txt)


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application and/or web site will be highly available by evenly distributing traffic, in addition to restricting unintended guests directly into the network.
- _Load Balancers provide a few different levels of security. For example, the main intended use of a load balancer, is to assist a website that is receives high volumes of web traffic. The load balancer will decide when one server is being overloaded by the traffic and will then redirect the traffic to another server within the same container, offloading the full stress, from the priority server. Which could result in Denial of Service(DoS). They recieve daily rule updates just like a virus scanner and the Load Balancer is also given it's own public IP. Having it's own Public IP, backed by a Jump Box, will make sure that the only traffic coming threw it are HTTP request. Making the web servers only accessable from a Jump Box. A Jump Boxes biggest advantages is allowing a one way connection with a server threw a SSH key, uniquely identified to a specific remote machine_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the traffic and system logs.
- _Filebeat is a program that assists in collection, generation, and the organization of log events pertaining to a specified server, including this ELK server. Specifically, Filebeat monitors any actions and changes within the system and marks them with a timestamp_
- _Metricbeat is assists in monitoring and makeing changes to a system that doesnt have Graphical User Inerface(GUI). Using Metricbeat you can monitor any processes running on that system that may be drawing from the systems resources_
