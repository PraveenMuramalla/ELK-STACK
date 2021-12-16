## Automated ELK Stack Deployment

"ELK" is the acronym for three open source projects: Elasticsearch, Logstash, and Kibana. Elasticsearch is a search and analytics engine. Logstash is a server‑side data processing pipeline that ingests data from multiple sources simultaneously, transforms it, and then sends it to a "stash" like Elasticsearch. Kibana lets users visualize data with charts and graphs in Elasticsearch. [source](https://www.elastic.co/what-is/elk-stack)

The files in this repository were used to configure the network depicted below.

![](https://user-images.githubusercontent.com/3822716/146291203-185a93ad-ef9c-481a-99c7-ef001da378a4.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML playbook files to only install certain pieces of it, such as skipping python if already installed or not executing metricbeat-playbook.yml 

*   elk-install\_playbook.yml
*   filebeat-playbook.yml
*   metricbeat-playbook.yml

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
| WEB-3 | DVWA Web Server | 10.0.0.7 | Ubuntu 18 |

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

*   _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
*   ...
*   ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats

This ELK server is configured to monitor the following machines:

*   _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:

*   _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:

*   _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:

*   Copy the **\_ file to \_**.
*   Update the \_\_\_\_\_ file to include...
*   Run the playbook, and navigate to \_\_\_\_ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_

*   _Which file is the playbook? Where do you copy it?_
*   _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
*   \_Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
