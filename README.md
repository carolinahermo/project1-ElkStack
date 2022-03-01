Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the project1-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

-Project1-playbook.yml file will load all four playbooks in succession, allowing for quick install on the virtual machines when they are active. 
-Pentest.yml it help to establishes the DVWA containers on the vms with in the White_Team virtual network. 
-Install-elk.yml connection from the Jump-Box virtual machine to install the ELK Server on the ELKStack virtual network vm. 
- Filebeat-playbook.yml let the installs filebeat monitoring program on the vm within the White_Team virtual network. 
- Filebeat-playbook.yml installs filebeat monitoring program on the virtual machine within the White_Team virtual networking.  


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build




The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

What aspect of security do load balancers protect? What is the advantage of a jump box? Load balancing is able to direct traffic efficiently is increased and better servers to fulfill the desired state of the CIA triad. 
The Jump-Box allows for more secure access and modification of vms, bolstering the integrity of the network, it also provides a buffer between direct access of the webservers, ensuring administrative control over task concerning those machines. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the event logs and system metrics.
 What does Filebeat watch for? Filebeat watches for log activity and hardest new log data from specified locations. 
- _TODO: What does Metricbeat record? The metrics from OS and services running on the server. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table 


| Name       | Funcion                              | Ip Address | Operating  system  |
|------------|--------------------------------------|------------|--------------------|
| Jump-Box   | gateway                              | 10.0.0.8   | Linux Ubuntu 18.04 |
| ELK Server | Server for ELK Stack                 | 10.1.0.4   | Linux Ubuntu 18.04 |
| Web-1      | WebServer- Docker Container for DVWA | 10.0.0.14  | Linux Ubuntu 18.04 |
| Web-2      | Server for Elk Stack                 | 10.0.0.15  | Linux Ubuntu 18.04 |








### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
 138.91.174.59 and private Ip unlisted


Machines within the network can only be accessed by ssh 10.0.0.8 private Ip on Jump-Box. Containers in Web-1 and Web-2 is allowed from allow-listed ips.

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accesible   | Allowed Ip Addresses                  |
|---------------|----------------------|---------------------------------------|
| Jump-Box      | Yes                  | 138.91.174.59 & Private Unlisted      |
| Web-1 & Web-2 | No (through LB only) | 10.0.0.14, 10.0.0.15 & 23.101.199.210 |
| ELKServer     | No                   | 10.1.0.4                              |
| Load Balancer | Yes                  |                                       |
 Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- TODO: What is the main advantage of automating configuration with Ansible?_

-Free: Ansible is an open-source tool.
	-Very simple to set up and use: No special coding skills are necessary to use Ansible’s playbooks (more on playbooks later).
	-Powerful: Ansible lets you model even highly complex IT workflows.
	-Flexible: You can orchestrate the entire application environment no matter where it’s deployed. You can also customize it based on your needs.
	-Agentless: You don’t need to install any other software or firewall ports on the client systems you want to automate. You also don’t have to set up a separate management structure.
	-Efficient: Because you don’t need to install any extra software, there’s more room for application resources on your server.

The playbook implements the following tasks:
- TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
	-Install docker.io
	-Install pip3
	-Install Docker python module
	-Increase virtual memory
	-Download and launch a docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
	10.0.0.14
	10.0.0.15 

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

	Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
    Filebeat is used to collect log files from specific files on remote machines.

		Examples of Filebeats can be files that are generated by Apache, Microsoft Azure tools, the Nginx web server, and MySQl databases.

	Metricbeat collects machine metrics.

		It is simply a measurement to tell analysts how healthy it is.

		Examples of Metricbeat can be CPU usage/Uptime
   
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
	- Copy the playbook file to Ansible Control Node.
	- Update the hosts file to include webserver and elk
	- Run the playbook, and navigate to Kibana (http:// 13.78.148.16/app/kibana#/home) to check that the installation worked as expected.

	---Filebeat---

	Copy the filebeat-configuration.yml file to /etc/ansible/roles/files.
	Update the filebeat-configuration.yml file to include the ELK private IP in lines 1106 and 1806.
	Run the playbook, and navigate to http://ELK public ip13.78.148.16:5601/ (13.78.148.16) to check that the installation worked as expected.
	
	---Metricbeat---
	Copy the metricbeat-configuration.yml file to /etc/ansible/roles/files.
	Update the metricbeat-configuration.yml file to include the ELK private IP in lines 62 and 96.
	Run the playbook, and navigate to http://ELK public ip13.78.148.16:5601/ (13.78.148.16) to check that the installation worked as expected.


_TODO: Answer the following questions to fill in the blanks:_
- Which file is the playbook? filebeat-playbook.yml
	- Where do you copy it? /etc/ansible/files
	- Which file do you update to make Ansible run the playbook on a specific machine? /etc/ansible/hosts file (IP of the Virtual Machines)
	-  How do I specify which machine to install the ELK server on versus which to install Filebeat on? I have to specify two separate groups in the etc/ansible/hosts file. One of the groups will be webservers which has the IPs of the VMs that I will install Filebeat to. The other group is named elkservers which will have the IP of the VM I will install ELK to.
	- _Which URL do you navigate to in order to check that the ELK server is running? http://ELK public 13.78.148.16

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
	-ssh username@ipaddressofjumpboxvm
	- sudo docker start (container name)
	- sudo docker attach (container name)
	- cd /etc/ ansible/
	- ls (to explore files on directory)
	- nano hosts (for setting up ips)
	- nano ansible.cfg (review the configuration)
	- nano /files/filebeat-config.yml
	- nano /files/metricbeat-config.yml 
	- nano metricbeat-playbook.yml
	- nano project.yml 
	- ansible-playbook /etc/ansible/project.yml
