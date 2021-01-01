## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(https://github.com/KoltenMount/Cloud_Network_project/blob/main/Diagrams/ELK_Stack_Deployment.pdf)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the (https://github.com/KoltenMount/Cloud_Network_project/tree/main/Ansible) folder may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly stable, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log events and system metrics.

The configuration details of each machine may be found below:

| Name     | Function          | IP Address | Operating System |
|----------|-------------------|------------|------------------|
| Jump Box | Gateway           | 10.0.0.4   | Linux            |
| Web-1    | DVWA Server       | 10.0.0.7   | Linux            |
| Web-2    | DVWA Server       | 10.0.0.8   | Linux            |
| Web-3    | DVWA Server       | 10.0.0.9   | Linux            |
| ELK      | Monitoring Server | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address:
- 73.78.111.39

Machines within the network can only be accessed by the Ansible container within the Jump Box Provisioner using the following IP: 
- 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Locally Accessible | Allowed IP Addresses |
|------------|---------------------|--------------------|----------------------|
| Jump Box   | Yes                 | No                 | 73.78.111.39         |
| Web-1      | No                  | Yes                | 10.0.0.4             |
| Web-2      | No                  | Yes                | 10.0.0.4             |
| Web-3      | No                  | Yes                | 10.0.0.4             |
| ELK Server | No                  | Yes                | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because configurations can be done in minutes without the potential of human error.

The playbook implements the following tasks:
- Updating apt cache and installing docker.io
- Installing python3-pip
- Installing image
- Increasing virtual memory
- Downloading and launching ELK container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(https://github.com/KoltenMount/Cloud_Network_project/blob/main/Images/docker_ps_elk.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.7
- 10.0.0.8
- 10.0.0.9

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects log data. An example would be a failed authentication attempt.
- Metricbeat records system metrics. This can include Network Traffic flow, CPU usage, load, and memory usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the 'https://github.com/KoltenMount/Cloud_Network_project/blob/main/Ansible/elk_playbook.yml' file to /etc/ansible/roles in your ansible node.
 
  - Inside your ansible node, navigate to /etc/ansible/roles using this command:
    'cd /etc/ansible/roles'
  - From this directory download the playbook by running:
    'curl https://raw.githubusercontent.com/KoltenMount/Cloud_Network_project/main/Ansible/elk_playbook.yml > elk_playbook.yml'

- Update the hosts file to include:

'[elkserver]

IP.of.your.ElkServer ansible_python_interpreter=/usr/bin/python3'
  
  - Navigate to your hosts file by running: 'cd /etc/ansible/hosts'
    Then run 'nano hosts' to edit the file and include the above information
    
- Run the playbook, and navigate to 'http://ip.of.your.elkserver:5601/app/kibana' to check that the installation worked as expected.
  
  - To run the playbook navigate back to the '/etc/ansible/roles' directory where the playbook exists and run:
    'ansible-playbook elk_playbook.yml'
