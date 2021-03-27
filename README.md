# CyberSecurity
DU - cybersecurity ELK project
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

#### Cloud Infrastructure Diagram:
https://github.com/shellycowan1986/CyberSecurity/blob/main/Diagrams/Cloud_Diagram.png


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

#### Filebeat playbook
https://github.com/shellycowan1986/CyberSecurity/blob/main/Ansible/filebeat-config.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- Load balancing is effective at preventing DDoS attacks. The advantage of the Jump Box is to provide a gateway router to your private network ensuring that all of your other machines in the network do not directly face the internet. This then provides a more secure network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
- Filebeat collects data about the file system, which files have changed and when they changed.
- Metricbeat collects machine metrics, such as uptime.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway        | 10.0.0.4  | Linux |   |
|----------|----------------|-----------|-------|---|
| Web-1    | DVWA Container | 10.0.0.9  | Linux |   |
| Web-2    | DVWA Container | 10.0.0.8  | Linux |   |
| Web-3    | DVWA Container | 10.0.0.10 | Linux |   |
| Elk-web  | Server         | 10.1.0.4  | Linux |   |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 67.176.54.4

Machines within the network can only be accessed by Jump Box.
- The ELK server can be accessed from the Web-1, Web-2, Web-3 and Jump Box machines.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
| Jump Box | No                  | 67.176.54.4             |
|----------|----                 |-------------------------|
| Web-1    | No                  | 10.0.0.4 / 67.176.54.4  |
| Web-2    | No                  | 10.0.0.4 /  67.176.54.4 |
| Web-3    | No                  | 10.0.0.4 /  67.176.54.4 |
| Elk-web  | No                  | 67.176.54.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
  The main advantage of automating configuration with Ansible is that it enables IT administrators the ability to automate your daily work tasks and give the administrator more time to focus on the needs of the business.

The 'install-elk.yml' playbook implements the following tasks:
- Configure Elk VM with Docker
- Install docker.io
- Install pip3
- Download and launch a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/81325191/112725659-ff2daf00-8ede-11eb-898e-140a874b5754.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.9
- Web-2 10.0.0.8
- Web-3 10.0.0.10

We have installed the following Beats on these machines:
- Filebeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects data about the file system, which files have changed and when they changed.
- Metricbeat collects machine metrics, such as uptime.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the YAML file to /etc/ansible.
- Update the /etc/ansible/hosts file to include host group, private IP address and the folliwng 'ansible_python_interpreter=/usr/bin/python3'
- Run the playbook, and navigate to curl localhost/setup.php to check that the installation worked as expected.

- The playbooks are listed as install-elk.yml / filebeat-playbook.yml / metricbeat-playbook.yml /ansible_config.yml and are meant to be copied into /etc/ansible directory.
- To make Ansible run the playbook on a specific machine, update the /etc/ansible/hosts file. Within this file, name groups using square brackets (currently contains '[webservers]' and '[elk]') surrounding the group-name and under the group-name, replace private IP's with your own respective IP's. You then use these group-names behind the "hosts:" field in the playbooks to specify which machines to apply the playbook to.
- To check if the ELK server is running, navigate to http://[your.VM.IP]:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
