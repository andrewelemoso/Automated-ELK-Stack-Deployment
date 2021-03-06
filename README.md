## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![ELK DIAGRAM](https://github.com/andrewelemoso/Automated-ELK-Stack-Deployment/blob/main/Diagrams/ELK_DIAGRAM.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the [Automated-ELK-STACK-Deployment](https://github.com/andrewelemoso/Automated-ELK-Stack-Deployment) file may be used to install only certain pieces of it, such as Filebeat.

[Filebeat Playbook](https://github.com/andrewelemoso/Automated-ELK-Stack-Deployment/blob/main/Ansible/Filebeat/filebeat-playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly **functional and redundant**, in addition to restricting **all access expect authorized administrative access** to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the **log files** and system **metrics.**

The configuration details of each machine may be found below.

| **Name** | **Function** | **IP Address**               | **Operating System** |
|----------|--------------|------------------------------|----------------------|
| Jbox     | Gateway      | 10.0.0.4(Private)//Public IP | Linux                |
| ELK      | Server       | 10.1.0.4(Private)//Public IP | Linux                |
| WEB-1    | Web Server   | 10.0.0.5(Private)            | Linux                |
| WEB-2    | Web Server   | 10.0.0.6(Private)            | Linux                |
| WEB-3    | Web Server   | 10.0.0.7(Private)            | Linux                |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the **Jbox (Jump Box) ** machine can accept connections from the Internet. Access to this machine is only allowed from the **Administrator's Public IP and all others the admin may add if needed.**


Machines within the network can only be accessed by **Jbox (10.0.0.4).**

A summary of the access policies in place can be found in the table below.

| **Name** | **Publicly Accessible** | **Allowed IP Address**                |
|----------|-------------------------|---------------------------------------|
| Jbox     | Yes                     | Admin's Public IP                     |
| ELK      | Yes                     | 10.0.0.4(Private) & Admin's Public IP |
| WEB-1    | No                      | 10.0.0.4(Private)                     |
| WEB-2    | No                      | 10.0.0.4(Private)                     |
| WEB-3    | No                      | 10.0.0.4(Private)                     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because **of the ability to use YAML playbooks which is the best alternative for configuration management/automation, It is also able to automate complex multi-tier IT application environemtns.**

The playbook implements the following tasks:
[ELK Install Playbook](https://github.com/andrewelemoso/Automated-ELK-Stack-Deployment/blob/main/Ansible/ELK/install-elk.yml)
- Download and Install Docker
- Download and Install Python3-pip
- Download and Install Docker
- Use Sysctl Module
- Download and launch a docker ELK container at Start Up

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps](https://github.com/andrewelemoso/Automated-ELK-Stack-Deployment/blob/main/Ansible/IMAGES/ELK-Docker-ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- WEB-1 (10.0.0.5)
- WEB-2 (10.0.0.6)  
- WEB-3 (10.0.0.7)         

We have installed the following Beats on these machines:
- Filebeat Module
- Metricbeat Module

These Beats allow us to collect the following information from each machine:
- Filebeat is used to collect log files from specific files on remote machines.
- Examples of Metricbeat can be CPU usage/Uptime.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the [Filebeat Configuration file](https://github.com/andrewelemoso/Automated-ELK-Stack-Deployment/blob/main/Ansible/Filebeat/Drew-filebeat-config.yml) file and [Filebeat Playbook file](https://github.com/andrewelemoso/Automated-ELK-Stack-Deployment/blob/main/Ansible/Filebeat/filebeat-playbook.yml) to `/etc/ansible`.
- Update the `/etc/ansible/hosts` file to include 
`[elk]
 10.1.0.4 ansible_python_interpreter=/usr/bin/python3`
 
- Run the playbook, and navigate to `http://[ELK-VM.Public.IP]:5601/app/kibana.`to check that the installation worked as expected.

**Successful Result should look just like these:**
![KIBANA](https://github.com/andrewelemoso/Automated-ELK-Stack-Deployment/blob/main/Ansible/IMAGES/Kibana.png)
![Filebeat](https://github.com/andrewelemoso/Automated-ELK-Stack-Deployment/blob/main/Ansible/IMAGES/Filebeat.png)
![Filebeat Sample](https://github.com/andrewelemoso/Automated-ELK-Stack-Deployment/blob/main/Ansible/IMAGES/Filebeat%20System%20Sample.png)
