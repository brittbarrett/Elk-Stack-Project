# Elk-Stack-Project

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(/Diagrams/RedTeam_Network.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the /etc/ansible folder may be used to install only certain pieces of it, such as Filebeat.

  - (/Ansible folder contains all necessary files)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
  - Load Balancers protect systems from Denial of Service (DDoS) attacks by shifting traffic. They distribute inbound network traffic among the connected web           servers inorder to mitigate DDos threats and attacks.
  
  - The Jump Box VM acts as a gateway as it it used to access and manage devices that live in two different security zones.  


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the jump box and system network.
- Filebeat is a tool used to send and centralize data. It monitors log files and locations that the user specifies, collects log events, and forwards these to       either ElasticLearsh or Logstash
- Metricbeat records statistics and metrics from the operating system and from services running on the server and forwards them to the output specified by the       user, such as Elasticsearch and Logstash. 

The configuration details of each machine may be found below.

| Name      | Function   | IP Address | Operating System |  
|-----------|------------|------------|------------------|
| Jump Box  | Gateway    | 10.0.0.4   | Linux            |   
| Elk Stack | Monitoring | 10.1.0.4   | Linux            |   
| Web-1     | Hosts      | 10.0.0.5   | Linux            |   
| Web-2     | Hosts      | 10.0.0.6   | Linux            |  

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 24.251.118.96

Machines within the network can only be accessed by ssh.
- The Jump-box-provisoner machine with an IP address of _52.158.232.233_ has access to the Elk server via ssh. 

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible? | Allowed IP Address                 | Allowed Ports | Allowed Protocols |
|----------------------|----------------------|------------------------------------|---------------|-------------------|
| Jump-Box-Provisioner | Yes                  | Home Public IP                     | 22            | TCP               |
| Elk-Server           | No                   | 10.0.0.4(JBP), 51.141.185.246(LB)  | 22, 80        | TCP               |
| Web-1                | No                   | 10.0.0.4(JBP), 51.141.185.246(LB)  | 22, 80        | TCP               |
| Web-2                | No                   | 10.0.0.4(JBP), 51.141.185.246 (LB) | 22, 80        | TCP               |
| Load Balancer        | Yes                  | Home Public IP                     | 80            | TCP               |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- it allows for more flexibility and repeatability, it only completes necessary tasks, allows for users to free up time as it is automated, and easy to set up. 

The playbook implements the following tasks:
- Installation of docker.io to run containers and python3-pip used to install Python software. 
- Increase virtual memory in order to use more memory so that the ELK container will actually run. The Ansible 'sysctl' module should be set to automatically run   in the event of VM restart.
- Installs the pip package docker. 
- Downloads Dockers container 'sebp/elk:761'
- Configures the container to start with the following port mappings: 
    - 5601:5601
    - 9200:9200
    - 5044:5044

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 VM: 10.0.0.5
- Web-2 VM: 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects data about syslogs, ssh attempts, sudo commands, and users and groups. 
- Metricbeat allows us to collect data like CPU usage, memory, network, and disk statistics from our host Web-1 and Web-2 servers. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible on your Jump Box server.
- Update the hosts file to include the 10.1.0.4 ansible_python_interpreter=/usr/bin/python. 
- Run the playbook, and navigate to http://Elk_External_IP>:5601/app/kibana to check that the installation worked as expected.

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
