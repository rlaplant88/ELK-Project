## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![ELK Project Diagram.png](https://github.com/rlaplant88/ELK-Project/blob/main/Diagrams/ELK%20Project%20Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.

  - The ansible-playbooks filebeat-playbook-webservers.yml and the elk-docker.yml are needed to create and implement the ELK-Server.

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

 -Load balancing protects the Availability portion of security in the CIA Triad.

The advantage of a JumpBox is that it controls access to the other machines by allowing connections from specific IP addresses and forwarding to those machines. Allowing the JumpBox to act as an originating port for launching Administrative Tasks.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- _Filebeat watches for log files/locations and collects log events_
- _Metricbeat records metric and statistical data from the operating system and from services running on the server_

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name                 | Function                            | IP Address             | Operating System     |
| -------------------- | ----------------------------------- | ---------------------- | -------------------- |
| Jump-Box-Provisioner | Gatway/Ansible                      | 10.0.0.7/65.52.120.244 | Linux (ubuntu 18.04) |
| Web-1                | Docker-DVWA (filebeat & metricbeat) | 10.0.0.5               | Linux (ubuntu 18.04) |
| Web-2                | Docker-DVWA (filebeat & metricbeat) | 10.0.0.6               | Linux (ubuntu 18.04) |
| ELK-Server           | ELK - Kibana                        | 10.1.0.4               | Linux (ubuntu 18.04) |
| Web-Load-Balancer  | Load Balancer  | 13.64.135.191  | Linux (ubuntu 18.04  |)

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _My Personal IP Address_

Machines within the network can only be accessed by SSH from the Jump-Box-Provisioner.
- _The only machines that are able to connect to the ELK-Server (10.1.0.4) is the Jump-Box-Provisioner from Private IP address (10.0.0.7) and My Personal IP._

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses      |
| -------------------- | ------------------- | ------------------------- |
| Jump-Box-Provisioner | No                  | My Personal IP            |
| Web-1                | No                  | 10.0.0.7                  |
| Web-2                | No                  | 10.0.0.7                  |
| ELK-Server           | No                  | 10.0.0.7 & My Personal IP |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _The main advantage of using Ansible to configure the ELK machine is that it is easily replicated. You can write one Playbook and configure multiple machines through the use of a single command after initial set up._

The playbook implements the following tasks:
- _Specifies a group of machines from the host file as well as the remote user for that machine_
- _Installs the following services_
  _docker.io_
  _python3-pip_
  _docker python module_
- _Increase system memory_
- _Download and Launch a docker ELK container over ports:
  _5601:5601_
  _9200:9200_
  _5044:5044_

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker_ps.JPG](https://github.com/rlaplant88/ELK-Project/blob/main/Ansible/docker_ps.JPG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _Web-1 - 10.0.0.5_
- _Web-2 - 10.0.0.6_

We have installed the following Beats on these machines:
- _We have installed Filebeat and Metric Beat onto the Web-1 and Web-2 machines and the logging information is being sent to the ELK-Server machine._

These Beats allow us to collect the following information from each machine:
- _Filebeat collects and monitors log files_
- _Metricbeat collects metrics and system statistics from the operating system and services running on the system_

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the configuration files to include the Private IP of the ELK-Server to the ElasticSearch and Kibana sections of the configuration file.
- Run the playbook, and navigate to ELK-Server public IP address (http://104.41.130.227:5601/app/kibana) to check that the installation worked as expected.



The commands needed to run the Ansible configuration for the ELK-Server are:
ssh azdmin@65.52.120.244
sudo docker container list -a (locate your ansible container name {clever_dhawan})
sudo docker start clever_dhawan
sudo docker attach clever_dhawan
sudo docker ps (to check to be sure the container is running)
cd etc/etc/ansible
ansible-playbook elk-docker.yml (configure the ELK-Server and starts the ELK container on the ELK-Server) wait a few minutes for the implementation of the ELK-Server 
cd etc/ansible/roles
ansible-playbook filebeat-playbook-webservers.yml (installs filebeat)
ansible-playbook metricbeat.yml (installs metricbeat)
open a new web browser (http://104.41.130.227:5601/app/kibana). This will bring up the Kibana Web Portal
 
