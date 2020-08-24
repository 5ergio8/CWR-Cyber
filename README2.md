## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Diagram of the Virtual Environment](https://github.com/5ergio8/CWR-Cyber/blob/master/Diagrams/Diagram2.0.jpg)

https://github.com/5ergio8/CWR-Cyber

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .YML file may be used to install only certain pieces of it, such as Filebeat.

Install-ELK.YML   Filebeat-Playbook.YML   Metricbeat-Playbook.YML   DVWA-Playbook.YML

This document contains the following details:
- Description of the Topology 
- Access Policies - Gaining access is done through the Provisioner VM by using SSH. 
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available and redundant, in addition to restricting all inbound traffic to the network.
    
The load balancer will help defend against DDoS attacks.

An advantage of having a jump box is to prevent all the VM's to be exposed to the public.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
-    What does filebeat watch for? Filebeat watches for log files and locations, also collects log events.
-   What does metricbeat record? Metricbeat records statistical data from the VM's to be able to sort through them with ease at a later point.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web1     | DVWA     | 10.0.0.5   | Linux            |
| Web2     | DVWA     | 10.0.0.6   | Linux            |
| Web3     | DVWA     | 10.0.0.8   | Linux            |
| Elk Server | ELK    | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 
 - 174.14.74.121

Machines within the network can only be accessed by SSH.

Which machine is allowedto access the ELK VM? What was its IP address?_
    The only machine able to connect to the ELk VM is the jumpbox provisioner with an IP adress of 52.149.149.53

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | 174.14.74.121        |
| Web1     | No                  | 10.0.0.4             |
| Web2     | No                  | 10.0.0.4             |
| Web3     | No                  | 10.0.0.4             | 
| ELK Server | No                | 10.0.0.4             |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
    The main advantage of automating configuration with Ansible is that it is easier to manage and perform. In case a machine goes down, deploying another one becomes super easy.

The playbook implements the following tasks:
 - Create the VM and specifics to it. In this case increasing the memory size.
 - Download and configure docker
 - Launching the container with certain ports to be accessed for security measure. Ports 5601,9200 and 5044 were used.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Docker is Running![alt text](
https://github.com/5ergio8/CWR-Cyber/blob/master/Diagrams/docker%20ps.jpg "Docker ps")


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
    10.0.0.6    10.0.0.7    10.0.0.9

We have installed the following Beats on these machines:_
    Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:

  - Metricbeat gathers metrics from the VM's. The gathered data can then be sorted and made into a visual if needed to be able to read it better.
  - Filebeat collects data logs. locations as well. Gathers the data and sends it to be sorted in a way that it can be understood easily.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Filebeat-Playbook.YML file to /etc/filebeat/filebeat.yml.
- Update the config file to include... the IP of the Elk-Server to the ElasticSearch and Kibana sections of the configuration file.
- Run the playbook, and navigate to the ELk server to check that the installation worked as expected.


- Which file is the playbook? Where do you copy it?_ the files with the playbook is called Filebeat-Playbook.YML and located in /etc/ansible/roles/
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ The files needed to update is called filebeat-config.yml and it is located in /etc/ansible/files/

- Which URL do you navigate to in order to check that the ELK server is running? http://40.122.52.101:5601/app/kibana

