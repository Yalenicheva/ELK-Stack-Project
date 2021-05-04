## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.



![image](https://user-images.githubusercontent.com/76926788/116769510-581ec480-aa02-11eb-8614-30298374fe7c.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat. The following playbooks were used to create and implement ELK server:

  - The Ansible-playbooks elk.yml
  - Filebeat-playbook.yml 
  - Metricbeat-playbook.yml 


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

What aspect of security do load balancers protect? What is the advantage of a jump box?

- Load Balancers protect against DDOS attacks and ensure availability which contributes to Availability aspect of security in regards of CIA Triad.
  
- The advantage of a jump box is a provide restricted access to your network environment. In this project only jump box has access to virtual network and allow HTTP traffic on port 80 to other Web VMs. Load balancer serves as origination point to connect to a network and distributes the traffic among VMs which protecs from single point of failure. 


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the operating system and system services.

What does Filebeat watch for?
 
- Filebeat monitors file logs, collects log events, and forwards them for indexing.
 
What does Metricbeat record?

- Metricbeat records metrics and statistics from an operating system and services running on a server. 

The configuration details of each machine may be found below.


| Name     | Function          | IP Address             | Operating System |
|----------|-------------------|------------------------|------------------|
| Jump Box | Gateway           | 10.0.0.4/103.40.20.158 | Linux            |
| Web-1    | DWVA Container    | 10.0.0.9               | Linux            |
| Web-2    | DVWA Container    | 10.0.0.10              | Linux            |
| Web-3    | DVWA Container    | 10.0.0.12              | Linux            |
| ELKVM    | ELK/Kibana Server | 10.1.0.4/20.81.40.154  | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

 - 104.40.20.158

Machines within the network can only be accessed by SSH via Jump Box.

Which machine did you allow to access your ELK VM? What was its IP address?

- Jump Box was allowed access the ELK VM. Its IP address was 10.0.0.4
  
 A summary of the access policies in place can be found in the table below.

|     Name                          |     Publicly   Accessible    |     Allowed   IP Addresses     |
|-----------------------------------|------------------------------|--------------------------------|
|           Jump      Box           |           YES/104.40.20.158  |           67.173.126.182       |
|           Web-1                   |           NO                 |           10.0.0.4             |
|           Web-2                   |           NO                 |           10.0.0.4             |  
|           Web-3                   |           NO                 |           10.0.0.4             | 
|           ELKVM                   |           NO                 |           20.81.40.154         |
 
 
 
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible?

- The main advantage of automating configuration with Ansible is ability to configure multiple machines with the single command after initial configuration which makes it faster and easier to use.  

The playbook implements the following tasks:
- Install Docker
- Specify which machines to ran a set of taks against [elk group]
yaml
		- hosts: elk
		- become: True
		- tasks:
			- name: Install Packages
			# Etc...
- Increase system memory: vm.max_map_count` to `262144
- Install the following apt packages:
  docker.io: The Docker engine, used for running containers.
  python3-pip: Package used to install Python software.
  docker: Python client for Docker. Required by Ansbile to control the state of Docker containers.
- Downloads the Docker container called sebp/elk:761. sebp is the organization that made the container. elk is the container and 761 is the version.
- Configures the container to start with the following port mappings:
			- 5601:5601
			- 9200:9200
			- 5044:5044
- Starts the container.

- Enables the docker service on boot, so that if you restart your ELK VM, the docker service start up automatically.
- Launching and Exposing the Container: use the command line to SSH into the ELK server and ensure that the sebp/elk:761 container is running by running docker ps.


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.  

https://github.com/Yalenicheva/ELK-Stack-Project/blob/main/Images/docker_ps_output.png

![image](https://user-images.githubusercontent.com/76926788/116770420-7a681080-aa09-11eb-9172-8165348f50e9.png)


### Target Machines & Beats

This ELK server is configured to monitor the following machines:

- Web-1 10.0.0.9
- Web-2 10.0.0.10
- Web-3 10.0.0.12

We have installed the following Beats on these machines:

- Filebeat-7.4.0-amd64.deb 
- Metricbeat-7.4.0-amd64.deb

These Beats allow us to collect the following information from each machine:

 - Filebeat monitors file logs, collects log events, and forwards them for indexing. Example of such logs is login attempts. 
 - Metricbeat records metrics and statistics from an operating system and services running on the server. Example is the CPU utilization. 
 

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:

For ELK VM Configuraiton:
- Copy the Ansible ELK Installation and VM Configuration
- Run the playbook using command: ansible-playbook install-elk.yml

For Filebeat:
-  Download filebeat playbook using curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml
- Copy the /etc/ansible/files/filebeat-config.yml to /etc/filebeat/filebeat-playbook.yml
- Update the filebeat-config.yml file to include the name, private IP address of ELK Server, state, and ports: 
  output.elasticsearch:
  hosts: ["10.1.0.4:9200"]
  username: "elastic"
  password: "changeme"

  ...
  setup.kibana:
  host: "10.1.0.4:5601
  
- Update filebeat-playbook.yml to include: https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb
- Run the filebeat-playbook.yml from /etc/ansible/roles directory and navigate to ELK Server GUI (Kibana): Logs>Add log data>System logs>Module Status to check that the installation worked as expected.

For Metricbeat:
- Download Metricbeat playbook using command: https://gist.githubusercontent.com/slape/58541585cc1886d2e26cd8be557ce04c/raw/0ce2c7e744c54513616966affb5e9d96f5e12f73/metricbeat
- Copy the /etc/ansible/files/metricbeat file to /etc/metricbeat/metricbeat-playbook.yml
- Update the the filebeat-playbook.yml to include:https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.4.0-amd64.deb 
- Update the metricbeat file rename to metricbeat-config.yml
- Run the playbook ansible-playbook metricbeat-playbook.yml and navigate to Kibana > Add Metric Data > Docker Metrics > Module Status to check that the installation worled as expected. 


Answer the following questions to fill in the blanks:

Which file is the playbook? Where do you copy it?

- The playbook file is called filebeat-playbook.yml, copy /etc/filebeat/filebeat.yml.

Which file do you update to make Ansible run the playbook on a specific machine?

- The hosts file. 

How do I specify which machine to install the ELK server on versus which to install Filebeat on?

- By specifying which host group (webservers/elkservers) the machines belong to.

Which URL do you navigate to in order to check that the ELK server is running?

- http://20.81.40.154:56 /app/kibana



As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.

•	ssh user@(IP Address)
•	docker run -ti container/ansible
•	change directory /etc/ansible
•	ssh-keygen to your web service
•	nano hosts (update IP on [webservers] [elkservers]
•	nano ansible.config to add user 
•	Create Ansible Playbook (
•	-name: Example Playbook
      hosts: webservers
      become: true
      tasks:
          -name: Install (name of the package)
           apt:
           force_apt_get: yes
           name: name of package
           state: present 








