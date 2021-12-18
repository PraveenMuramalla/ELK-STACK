## Automated ELK Stack Deployment

"ELK" is the acronym for three open source projects: Elasticsearch, Logstash, and Kibana. Elasticsearch is a search and analytics engine. Logstash is a server‑side data processing pipeline that ingests data from multiple sources simultaneously, transforms it, and then sends it to a "stash" like Elasticsearch. Kibana lets users visualize data with charts and graphs in Elasticsearch. [source](https://www.elastic.co/what-is/elk-stack)

The files in this repository were used to configure the network depicted below.

![](https://user-images.githubusercontent.com/3822716/146645364-9969bf66-022d-493b-9ed6-201f54a7d926.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML playbook files to only install certain pieces of it, such as skipping python if already installed or not executing metricbeat-playbook.yml 

*   [install-elk.yml](https://github.com/PraveenMuramalla/ELK-STACK/blob/main/Ansible/install-elk.yml)
*   [filebeat-playbook.yml](https://github.com/PraveenMuramalla/ELK-STACK/blob/main/Ansible/filebeat-playbook.yml)
*   [metricbeat-playbook.yml](https://github.com/PraveenMuramalla/ELK-STACK/blob/main/Ansible/metricbeat-playbook.yml)

This document contains the following details:

*   Description of the Topology
*   Access Policies
*   ELK Configuration
    *   Beats in Use
    *   Machines Being Monitored
*   How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D\*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting unauthorized access to the network. By implementing load balancer we ensure we take care of the "Availability" part of the CIA triad. Load balancers also helps to secure the servers from DDoS attacks. The implementation makes use of a jumbox which allows the administrator to access the web servers from a jumpbox only. This setup ensures the webservers are secured from cyber attacks.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

*   Filebeat monitors and collect log files or filesystem, you can find graphs depicting the traffic to your server, the amount of unique connections, and the type of errors received by these connections. As well as the source IP, geolocation, and url they accessed it from.
*   Metricbeat allows you to collect and analyze the metrics of your applications. Metricbeat will show Inbound and Outbound traffic, Memory usage, Disk usage, CPU usage, In and Out packet loss, and many other metrics.

The configuration details of each machine may be found below.

| Name | Function | IP Address | Operating System |
| --- | --- | --- | --- |
| Jump Box | Gateway | 10.0.0.4 | Ubuntu 18 |
| ELK | ELK Server | 10.1.0.4 | Ubuntu 18 |
| WEB-1 | DVWA Web Server | 10.0.0.5 | Ubuntu 18 |
| WEB-2 | DVWA Web Server | 10.0.0.6 | Ubuntu 18 |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from Public IP of the Admin : SSH ( port 22)

Machines within the network can only be accessed by Jump Box .

*   The Jumpbox machine is allowed access to the ELK VM.
    *   10.0.0.4 : SSH (port 22)
    *   Public IP of Admin ( port 5601 )

A summary of the access policies in place can be found in the table below.

| Name | Publicly Accessible | Allowed IP Addresses |
| --- | --- | --- |
| Jump Box | YES | Public IP of Admin : SSH ( port 22 ) |
| ELK ( Server ) | NO | Jump Box ( 10.0.0.4 ) |
| ELK ( ElasticWebApp ) | YES | Public IP of Admin : TCP ( port 5601 ) |
| WEB-1 ( Server ) | NO | Jump Box ( 10.0.0.4 ) |
| WEB-2 ( Server ) | NO | Jump Box ( 10.0.0.4 ) |
| WEB-1 ( DVWA ) | YES | Public IP of Admin via Load Balancer |
| WEB-2 ( DVWA ) | YES | Public IP of Admin via Load Balancer |

### Elk Configuration

Ansible was used to automate configuration of the ELK Server setup. No configuration was performed manually, which is advantageous because, it helps to achieve the concept of Infrastructure as code.

*   It allows quick and easy deployment of applications using playbooks
*   We can setup the same server setup in any network with exact configuration.
*   It helps not having to backup the Server

The playbook implements the following tasks:

*   Install Docker.io
*   Install Python3-pip
*   Install docker module
*   Increase & use more virtual memory
*   Download and launch the Docker ELK container

### Target Machines & Beats

This ELK server is configured to monitor the following machines:

*   10.0.0.5 ( Web-1) : DVWA
*   10.0.0.6 ( Web-2) : DVWA

We have installed the following Beats on these machines:

*   filebeat-7.6.1-amd64.deb
*   metricbeat-7.6.1-amd64.deb

These Beats allow us to collect the following information from each machine:

*   Filebeat helps to collect Apache logs and it also indicates information that has been modified and when the modification took place
*   Metricbeat Metricbeat watches for change in system metrics such as change in CPU usage,SSH login attempts, and RAM statistics.

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:

*   Copy the [install-elk.yml](https://github.com/PraveenMuramalla/ELK-STACK/blob/main/Ansible/install-elk.yml) to /etc/ansible.
*   Update the [hosts](https://github.com/PraveenMuramalla/ELK-STACK/blob/main/Ansible/hosts) file to include the Elk-VM IP under \[elk\].
*   Run the playbook install-elk.yml, and navigate to [http://\<public ip of elk>:5601/app/kibana](http://52.161.65.211:5601/app/kibana) to check that the installation worked as expected.

The playbook files are:

*   [install-elk.yml](https://github.com/PraveenMuramalla/ELK-STACK/blob/main/Ansible/install-elk.yml) - Install ELK Server
*   [filebeat-playbook.yml](https://github.com/PraveenMuramalla/ELK-STACK/blob/main/Ansible/filebeat-playbook.yml) - Install and configure Filebeat on Elk Server and DVWA servers
*   [metricbeat-playbook.yml](https://github.com/PraveenMuramalla/ELK-STACK/blob/main/Ansible/metricbeat-playbook.yml) - Install and configure Metricbeat on Elk Server and DVWA servers

Where do you copy it?

*   /etc/ansible/

Update to make Ansible run the playbook on a specific machine?

*   /etc/ansible/hosts to configure \[webservers\] and \[elk\] with ip addresses of the machines

Specify which machine to install the ELK server , Filebeat and MetricBeaton?

In /etc/ansible/hosts configure IP Address for ElkServers ( elk ) or FileBeat (webservers)

Which URL do you navigate to in order to check that the ELK server is running?

http://\<public ip of elk>:5601
