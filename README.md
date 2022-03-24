## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![File Path to Diagram](/Diagram/Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

  !(/Ansible/Filebeat/filebeat-playbook.yml)

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
- _: A load balancer distributes the network traffic, preventing an overload on a server. A jumobox allows to manage access and security.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- _Filebeat monitors log files and collects log events
- _Metricbeat collects metrics from the system and services running on the server._

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function        | IP Address | Operating System     |
|----------|-----------------|------------|----------------------|
| Jump Box | Gateway         | 10.0.0.4   | Linux                |
| Web-1    | Virtual Machine | 10.0.0.5   | Linux (ubuntu 18.04) |
| Web-2    | Virtual Machine | 10.0.0.6   | Linux (ubuntu 18.04) |
| Elk-VM   | Virtual Machine | 10.1.0.4   | Linux (ubuntu 18.04) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _76.170.213.138

Machines within the network can only be accessed by SSH.
- _Elk-VM has access to JumpBoxProvisioner. It's IP address is 10.0.0.4_

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | 76.170.213.138       |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |
| Elk-VM   | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _When adding new Virtual Machiines, we can apply the same playbooks that were already mad; automation of code._

The playbook implements the following tasks:
- Install Docker
- Install python3-pip
- DOcker Module
- Icrease virtual memory
- Install Elk Container
- Enable Docker to start on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

  ![File Path to screenshot](/Ansible/Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _10.0.0.5
- _10.0.0.6

We have installed the following Beats on these machines:
- _Filebeat and Metricbeat_

These Beats allow us to collect the following information from each machine:
- _Filebeat collects audit logs, deprecation logs, gc logs, server logs, and slow logs.
   Metricbeat collect the metric from the OS and from services running on the server_

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml file to /etc/filebeat/filebeat.yml.
- Update the hosts file to include your destination IP
- Run the playbook, and navigate to http://[Your Elk IP]:5601/app/kibana to check that the installation worked as expected.