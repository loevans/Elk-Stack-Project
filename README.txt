## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _playbook____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

/etc/ansible/install-elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _effeciant____, in addition to restricting _traffic____ to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

Load balancing plays an important security role; the off-loading finction of a load balancer defends against DDos attacks by spreading the traffic across the network environment.  A jump box is a secure computer that connects with a single node access point.  It sits in front of other machines that are not exposed to the public internet.  The jump box has only one path in via SSH, and no other protocols are allowed outbound to the internet or into the corporate network. A jump box is also a reasonable solution when some of your users either have no direct office or data center access.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _logs____ and system _traffic____.

- _TODO: What does Filebeat watch for? Filebeat helps generate and organize log files to send to Logstash and Elasticsearch essentially monitoring log files for changes and events.

- _TODO: What does Metricbeat record? Metricbeat collects machine metrics from the OS system and from services running on the target server, such as CPU usage, memory and uptime.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Ubuntu 18.04     |
| Web1     | Server   | 10.0.0.8   | Ubuntu 18.04     |
| Web2     | Server   | 10.0.0.9   | Ubuntu 18.04     |
| Elk      | Server   | 10.1.0.5   | Ubuntu 18.0      |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _Jump Box Provisioner____ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_public ip address of the Jump Box Provisioner - 52.186.16.122

Machines within the network can only be accessed by _SSH____.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_The ELK VM is accessed by SSH from the Jump Box Provisioner 10.0.0.7

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 52.186.16.122        |
| Web1     | No                  |                      |
| Web2     | No                  |                      |
| Elk      | Yes                 | 10.1.0.5             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_The main advantage of automating configuration with Ansible is the simplify complex tasks that can be time consuming, therefore 

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
Install docker.io
Install python3-pip
Increase virtual memory command :sysctl -w vm.max_map_count=262144
Download nad launch a dolcker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

 

Images/docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring

Web1 10.0.0.8
Web2 10.0.0.9

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._Filebeat collects log files and logs information including any changes made and when.  Any attack leaves a trace that can be followed and investigated using logs.  Metricbeat collects machine metrics such as CPU or memeory or data related to services running on the server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _playbook____ file to _/etc/ansible/____.
- Update the _config____ file to include the private IP address of the Elk VM.
- Run the playbook, and navigate to _Kibana___ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? .yml file Where do you copy it?_copy the file to /etc/ansible/hosts (nano /etc/ansible/hosts)
Add a [elk] group to the hosts file:
	# /etc/ansible/hosts
 	[webservers]
	10.0.0.8 ansible_python_interpreter=/usr/bin/python3
 	10.0.0.9 ansible_python_interpreter=/usr/bin/python3
 	[elk]
	10.1.0.4 ansible_python_interpreter=/usr/bin/python3

- _Which file do you update to make Ansible run the playbook on a specific machine? You would update the hosts file. How do I specify which machine to install the ELK server on versus which to install Filebeat on?_You would specify a group [elk] or [webservers] and update the hosts file in /etc/hosts/
- _Which URL do you navigate to in order to check that the ELK server is running? http://20.225.56.168:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

ansible-playbook


