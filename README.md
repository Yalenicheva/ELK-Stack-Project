## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.


![image](https://user-images.githubusercontent.com/76926788/116769510-581ec480-aa02-11eb-8614-30298374fe7c.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.

  - The Ansible-playbooks elk.yml, and the filebeat-playbook.yml are needed to create and implement ELK server.


This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly avaliable, in addition to restricting the access to the network.

- What aspect of security do load balancers protect? What is the advantage of a jump box?

  Load Balancers protect against DDOS attacks and ensure availability which contributes to Availability aspect of security in regards of CIA Triad.
  
  The advantage of a jump box is a provide restricted access to your network environment. Only jump box has access to virtual network and serves as origination point to connect   to a network. 


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the operating system and system services.

- What does Filebeat watch for?
 
Filebeat monitors file logs, collects log events, and forwards them for indexing.
 

- What does Metricbeat record?

Metricbeat records metrics and statistics from an operating system and services running on a server. 



