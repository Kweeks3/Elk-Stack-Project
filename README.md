# Elk-Stack-Project

KWeeks Vanderbilt GitLab

# Azure Network and Elk Stack

Below are all images and files compiled to create and run the Elk Stack Network with the 
Azure Lab Environment.

![Cloud_Security](https://user-images.githubusercontent.com/97552776/166241269-980481e6-f54e-466b-81a5-2ea29df0f8ff.JPG)

These files were all used in order to complete the Azure deployment. Starting from the Elk installation to the Filebeat and Metricbeat playbooks used in order to run 
specific parts of the stack server. 

* [Elk Installation Playbook](./Elk-Stack-Project/Ansible/install-elk.yml) installs the Elk server.
* [Filebeat Playbook](filebeat-playbook.yml) installs Filebeat to the Elk VM.
* [Metricbeat Playbook](metricbeat-playbook.yml) installs Metricbeat to the Elk VM.

# Network Description

Previously, a Cloud Network system was set up within the Azure Lab environment along with a newly created Network Security and Monitoring system. 
The purpose of the Elk Server is to monitor the Load-Balancer which gives network access to the user while heavily restricting access to those outside of it. 
Everything is done from a docker container within a Provisioned Jump Box which allows the user-only to have access to the network while the Load-Balancer keeps outside individuals from SSHing to the VMs while accessing the DVWA (Damn Vulnerable Web Application) from the internet. 

With the Elk Server installed, the modules **Filebeat* and **Metricbeat* were then installed to monitor system logs (Filebeat) and CPU performance (MetricBeat).
