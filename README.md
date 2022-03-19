## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Images/diagram_azure_elk_network.png](https://github.com/loevans/Elk-Stack-Project/blob/main/Images/diagram_azure_elk_network.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook YML file may be used to install only certain pieces of it, such as Filebeat.

  - [install-elk.yml](https://github.com/loevans/Elk-Stack-Project/blob/main/Ansible/install-elk.yml.txt)
  - [filebeat-playbook.yml](https://github.com/loevans/Elk-Stack-Project/blob/main/Ansible/filebeat-playbook.yml.txt)
  - [metricbeat-playbook.yml](https://github.com/loevans/Elk-Stack-Project/blob/main/Ansible/metricbeat-playbook.yml.txt)
 

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly avaliable, in addition to restricting access to the network.
- What aspect of security do load balancers protect? Load balancing plays an important security role protecting  The off-loading function of a load balancer defends against DDos attacks by spreading the traffic across the network environment ultimately easing the impact of the attack on your infrastructure. The load balancer shifts the attack traffic tp a public cloud provider.
- What is the advantage of a jump box? A jump box is a secure computer that connects with a single node access point and serves as a gateway to gain entry into a remote network.  It sits in front of other machines that are not exposed to the public internet.  The jump box has only one path in via SSH, and no other protocols are allowed outbound to the internet or into the corporate network. A jump box is also a reasonable solution when some of your users either have no direct office or data center access.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resources.

-What does Filebeat watch for? Filebeat helps generate and organize log files to send to Logstash and Elasticsearch essentially monitoring log files for changes and events.

-What does Metricbeat record? Metricbeat collects machine metrics from the OS system and from services running on the target server, such as CPU usage, memory and uptime.


The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.7   | Linux (Ubuntu)   |
| Web1     | Server   | 10.0.0.8   | Linux (Ubuntu)   |
| Web2     | Server   | 10.0.0.9   | Linux (Ubuntu)   |
| Elk      | Server   | 10.1.0.5   | Linux (Ubuntu)   |
 
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Add whitelisted IP addresses: 52.186.16.122

Machines within the network can only be accessed by the Jump Box (SSH).
- Which machine did you allow to access your ELK VM? Jump Box Provisioner
- What was its IP address? 10.0.0.7

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 52.186.16.122        |
| Web1     | No                  | 10.0.0.8             |
| Web2     | No                  | 10.0.0.9             |
| Elk      | Yes                 | 20.225.56.168        |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it reduces configuration errors and installation and update can be streamlined.  

- What is the main advantage of automating configuration with Ansible? The main advantage of automating configuration with Ansible is to simplify complex tasks that can be time consuming. Ansible is simple, powerful and agentless.

The playbook implements the following tasks: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.
- Install docker.io: Installs the core docker code to the remote server
- Install python3-pip: pip is the standard packet management system for Python
- Docker Module: Tells the previous PIP module to install the necessary docker compenent modules.
- Increase virtual memory command :sysctl -w vm.max_map_count=262144
- Download and launch a docker elk container: This downloads the docker container for ELK

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
![Images/docker_ps_output](https://github.com/loevans/Elk-Stack-Project/blob/main/Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

-   10.0.0.8
-   10.0.0.9
-   10.1.0.5

We have installed the following Beats on these machines:

-	Filebeat
-	Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat collects log files and logs information including any changes made and when.  Any attack leaves a trace that can be followed and investigated using logs.
- Metricbeat collects machine metrics such as CPU or memeory or data related to services running on the server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the provided configuration file for filebeat and metricbeat to the Ansible container.
- Update the configuration file /etc/ansible/files/filebeat-conf.yml file to include the ELK server's IP address. 
- Run the playbook, and navigate to http://[your_elk_server_ip];5601/app/kibana to check that the installation worked as expected.

  - Verify that your playbook is completing Steps 1-4.
  - On the same page, scroll to Step 5: Module Status and click Check Data.
  - Scroll to the bottom and click on Verify Incoming Data.

Answer the following questions to fill in the blanks:
- Which file is the playbook? Playbooks always carry the .yml extension and begin with --- on the first line to signify that it is a YAML file.
  - filebeat-playbook.yml is located in /etc/ansible/roles/
  - metricbeat-playbook.yml is located in /etc/ansible/roles/ 
 
- Where do you copy it? Copy to /etc/ansible/files/filebeat-config.yml to /etc/filebeat/filebeat.yml

- Which file do you update to make Ansible run the playbook on a specific machine? You would update the /etc/ansible/hosts file. How do I specify which machine to install the ELK server on versus which to install Filebeat on? You would specify which machine to install by assigning a group [elk] or [webservers] and updating with IP addresses of webservers and elk servers to update the hosts file.

-![Images/hosts.PNG](https://github.com/loevans/Elk-Stack-Project/blob/main/Images/hosts.PNG)

- Which URL do you navigate to in order to check that the ELK server is running? http://20.225.56.168:5601/app/kibana, http://[your_elk_server_ip];5601/app/kibana  

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.

⦁	run and copy the playbook: run curl https://github.com/loevans/Elk-Stack-Project/blob/main/Ansible/install-elk.yml > /etc/ansible/roles/install-elk-yml

⦁	Update the hosts file: nano /etc/ansible/hosts and assign a [group] and updating your destination IP address.

⦁	Run the playbook using the command: ansible-playbook /etc/ansible/roles/install-elk.yml
⦁	Check your installation is running by going to http://[your_elk_server_ip];5601/app/kibana in a browser. Your output should be similar to: 
![Images/kibana.PNG](https://github.com/loevans/Elk-Stack-Project/blob/main/Images/kibana.PNG)

⦁	Install Filbeats:	 Download the playbook with the following command: curl https://github.com/loevans/Elk-Stack-Project/blob/main/Ansible/filebeat-playbook.yml > /etc/ansible/roles/filebeat-playbook.yml

⦁	Run the playbook using the command: ansible-playbook /etc/ansible/roles/filebeat-playbook.yml

⦁	Repeat these steps for Metricbeat setup. 

⦁	click on Getting started, click on DEB and then scroll down and click on Module status.  Click on System logs dhashboard and you should see the following information:

![kibana_system_log_data](https://user-images.githubusercontent.com/93744925/158880414-07d6ca44-0cbd-417c-9c88-7d6402c47c63.PNG)




