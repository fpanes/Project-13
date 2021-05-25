# Project-1
ELK Stack Project
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![github-small](https://github.com/fpanes/Project-13/blob/main/Diagrams/FrancisPanes_CloudSecurity.png) 

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

  - [Ansible](https://github.com/fpanes/Project-1/tree/main/Ansible)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
- What aspect of security do load balancers protect? 
  - Availability, Web Traffic, Web Security 
- What is the advantage of a jump box? 
  - Automation, Security, Network Segmentation, Access Control


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- What does Filebeat watch for? 
  - Filebeat monitors the log files and collects log events, and sends to Elasticsearch or Logstash for indexing.
- What does Metricbeat record? 
  - Metricbeat takes the metrics and statistics that it collects and sends them to Elasticsearch or Logstash.

The configuration details of each machine may be found below.
Note: Use the (http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table.

| Name     | Function   | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.4   | Linux            |
| Web-1    | Web Server | 10.0.0.5   | Linux            |
| Web-2    | Web Server | 10.0.0.6   | Linux            |
| ELK      | ELK Stack  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Local Machine Public IP

Machines within the network can only be accessed by Jumpbox.
- Jumpbox 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses              |
|---------------|---------------------|-----------------------------------|
| Jump Box      | No                  | Local Machine Public IP           |
| Web-1         | No                  | 10.0.0.5                          |
| Web-2         | No                  | 10.0.0.6                          |
| ELK           | No                  | 10.1.0.4/Local Machine Public IP  |
| Load Balancer | No                  | Local Machine Public IP           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
Ansible lets you easily deploy apps

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- SSH to Jumpbox
- Install docker.io
- Install pthyon-pip
- Create playbooks
- SSH into ELK and test

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
10.0.0.4
10.0.0.5

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
ELK, Web-1, Web-2 
Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers. Filebeat monitors the log files or locations that you specify, gathers log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metric is a lightweight shipper that you can install on your servers to periodically gather metrics from the operating system and form services running on the server. Metricbeat takes the metrics and statistics that it gathers and ships them to the output that you specify, such as Elasticsearch or Logstash.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the /etc/ansible/files/filebeat-config.yml file to /etc/filebeat/filebeat-playbook.yml.
- Update the filebeat-config.yml file to include 
output.elasticsearch:
  #Array of hosts to connect to.
 hosts: ["10.1.0.4:9200"]
  username: "elastic"
  password: "changeme” 

 setup.kibana:
  host: "10.1.0.4:5601"
- Run the playbook, and navigate to Kibana / Logs : Add log data / System logs / 5:Module Status to check that the installation worked.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_ .yml and to /files
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ The config.yml 
- _Which URL do you navigate to in order to check that the ELK server is running?
sysadmin@10.1.0.4: curl Myhomeip:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
