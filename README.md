# Elk-Stack-Project

KWeeks Vanderbilt GitLab

# Azure Network and Elk Stack

Below are all images and files compiled to create and run the Elk Stack Network with the 
Azure Lab Environment.

![Cloud_Security](https://user-images.githubusercontent.com/97552776/166241269-980481e6-f54e-466b-81a5-2ea29df0f8ff.JPG)

These files were all used in order to complete the Azure deployment. Starting from the Elk installation to the Filebeat and Metricbeat playbooks used in order to run 
specific parts of the stack server. 

* [Elk Installation Playbook](Ansible/install-elk.yml) installs the Elk server.
* [Filebeat Playbook](Ansible/filebeat-playbook.yml) installs Filebeat to the Elk VM.
* [Metricbeat Playbook](Ansible/metricbeat-playbook.yml) installs Metricbeat to the Elk VM.

# Network Description

Previously, a Cloud Network system was set up within the Azure Lab environment along with a newly created Network Security and Monitoring system. 
The purpose of the Elk Server is to monitor the Load-Balancer which gives network access to the user while heavily restricting access to those outside of it. 
Everything is done from a docker container within a Provisioned Jump Box which allows the user-only to have access to the network while the Load-Balancer keeps outside individuals from SSHing to the VMs while accessing the DVWA (Damn Vulnerable Web Application) from the internet. 

With the Elk Server installed, the modules **Filebeat** and **Metricbeat** were then installed to monitor system logs (Filebeat) and CPU performance (MetricBeat).

A Total of 3 VMs with a Jump Box to access them was used in this lab environment. The following and their functions are..

| Name                 | Function    | IP Address |
| -------------------- | ----------- | ---------- |
| JumpBox-Provisioner1 | Gateway     | 10.0.0.4   |
| Web1                 | DVWA Server | 10.0.0.5   |
| Web2                 | DVWA Server | 10.0.0.6   |
| ElkVM                | Elk Stack   | 10.1.0.4   |

# Access Policies

A Jump Box was used to be able to connect and accept connections from the internet while only allowing access to this machine from a personal home IP address. The other VMs within the network were protected and not accessible to the internet due to the Jump Box and it's access policies. 

All of the following VMs are accessible through SSH of the Jump Box. The table below shows the access policies..

| Name                 | Public Access | Approved IP    |
| -------------------- | ------------- | -------------- |
| JumpBox-Provisioner1 | Yes           | 98.193.XXX.XXX |
| Web1                 | No            | 10.0.0.4       |
| Web2                 | No            | 10.0.0.4       |
| ElkVM                | No            | 10.0.0.4       |

# Configuring the Elk Stack

Similar to the deployment of the docker container, Ansible is used to configure the Elk Stack as well. From the installation to the modules used within the server, each of them required a different playbook to properly configure the Elk Stack. 

The following 3 playbooks below were used in this process..

* [Install Elk Playbook](Ansible/install-elk.yml) Use the 'apt' command to install docker.io and python3-pip. Afterwards, use 'pip' to install docker python module. The Elk Stack's docker container should be ready to install and launch at this point. 
 
* [Install Filebeat Playbook](Ansible/filebeat-playbook.yml) Download Filebeat and copy the configuration. Set up and enable the Filebeat module then start the service.

* [Install Metricbeat Playbook](Ansible/metricbeat-playbook.yml) Download Metricbeat and copy the configuration. Set up and enable the Metricbeat module then start the service.

# Affected Machines and Modules

Web1 and Web2 machines within the Cloud Network are the targetted machines being monitored by the Elk Stack Server. Both Filebeat and Metricbeat are installed to observe and collect information from the VMs. As mentioned before, **Filebeat** monitors system logs and failure attempts of processes within the network. **Metricbeat** collects data from the VMs CPU processes such as usage and memory. 

# Ansible Playbook

Before the Elk Stack's Playbooks can be deployed, Ansible must already be configured from the docker container. In order to do so, you will SSH into the Ansible container from the Jump Box and copy the 3 playbooks to insert within the hosts file of your Ansible container. Once in, you will create a new Elk webserver that looks similar to this within the hosts file..

**[webservers]**
10.0.0.5 ansible_python_interpreter=/usr/bin/python3
10.0.0.6 ansible_python_interpreter=/usr/bin/python3

[elk]
10.1.0.4

