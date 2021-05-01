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

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.


| Name     | Function          | IP Address             | Operating System |
|----------|-------------------|------------------------|------------------|
| Jump Box | Gateway           | 10.0.0.4 103.40.20.158 | Linux            |
| Web-1    | DWVA Container    | 10.0.0.9               | Linux            |
| Web-2    | DVWA Container    | 10.0.0.10              | Linux            |
| Web-3    | DVWA Container    | 10.0.0.12              | Linux            |
| ELKVM    | ELK/Kibana Server | 10.1.0.4 20.81.40.154  | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- Add whitelisted IP addresses

  104.40.20.158

Machines within the network can only be accessed by SSH via Jump Box.

- Which machine did you allow to access your ELK VM? What was its IP address?

  Jump Box was allowed access the ELK VM. Its IP address was 10.0.0.4
  
 A summary of the access policies in place can be found in the table below.

|     Name                          |     Publicly   Accessible    |     Allowed   IP Addresses     |
|-----------------------------------|------------------------------|--------------------------------|
|           Jump      Box           |           YES                |           67.173.126.182       |
|           Web-1                   |           NO                 |           10.1.0.4 10.0.0.4    |
|           Web-2                   |           NO                 |           10.1.0.4 10.0.0.4    |
|           Web-3                   |           NO                 |           10.1.0.4 10.0.0.4    |
|           ELKVM                   |           YES                |            67.173.126.182      |
 
 
 
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?

  The main advantage of automating configuration with Ansible is ability to configure multiple machines with the single command after initial configuration which makes it easier to use.  

The playbook implements the following tasks:
- Install Docker
- Create & Attach a container
- Install Filebeat on Web VMs
- Create Filebeat configuration file
- Create Filebeat installation play
- Verify the installation & playbook 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.  

