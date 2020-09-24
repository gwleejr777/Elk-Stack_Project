## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Image of Red Team Resource Group and Elk Stack](/images/Elk_Stack_Red_Team-RG.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the __playbook.yml__ file may be used to install only certain pieces of it, such as Filebeat.

  - __install-elk.yml__

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly __available__, in addition to restricting __access__ to the network.

- What aspect of security do load balancers protect?
- __Load Balancers protect availability of the VMs. Protects against DDOS attacks and help balance the load on servers. Provide redundancy and reduce or eliminate downtime in the event a server goes down. It also protects the internal network by providing a public IP to the Load Balancer and hides the other machines on the internal network__. 

What is the advantage of a jump box?
- __It allows access to manage all devices in the network. It's allows the server to pivot to another server and provides an added layer of security to the network__

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the __files__ and __system__ logs.
- What does Filebeat watch for? __Filebeat collects system logs and fowards them to elasticsearch for review__
- What does Metricbeat record? __Metricbeat gathers metric and statistics and sends the data to the output specified, such as elasticsearch.__

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function       |IP Address| Operating System |
|----------|----------------|The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System   |
|----------|----------|------------|------------------- |
| Jump Box | Gateway        | 10.0.0.8   | Linux Ubuntu 18.04 |
| Web-1    | Webserver/DVWA | 10.0.0.4   | Linux Ubuntu 18.04 |
| Web-2    | Webserver/DVWA | 10.0.0.5   | Linux Ubuntu 18.04 |
| Elk-VM   | Log Server     | 10.1.0.4   | Linux Ubuntu 18.04 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the __Jump Box__ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- __My Home IP Address: xx.xxx.xx.xxx__

Machines within the network can only be accessed by __Jump Box w/Ansbile + Docker__.
- Which machine did you allow to access your ELK VM? __I allowed my Jump Box Docker container 'funny_Borg' to access my ELK VM__ 
- What was its IP address? __Private IP: 10.1.0.4__

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses             |
|----------|---------------------|----------------------------------|
| Jump Box | Yes                 | 13.84.200.161, My Home IP Address 
|  Web-1   | No                  | 10.0.0.8
|  Web-2   | No                  | 10.0.0.8                     
|  Elk-VM  | No                  | 10.0.0.8, My Home IP Address?  

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible? __The main advantage is the reduction of resources needed and amount of time to it takes to launch VMs across a network__.

The playbook implements the following tasks:
- __name: Install docker.io__
- __name: Install python3-pip__
- __name: Install Docker module__
- __name: Increase virtual memory__
- __name: Download and launch a docker elk container__

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Image of Docker ps output](images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- __Web-1 10.0.0.4__
- __Web-2 10.0.0.5__

We have installed the following Beats on these machines:
- __Filebeats & Metricbeats__

These Beats allow us to collect the following information from each machine:
- __Filebeats collects system log events__
- __Metricbeat collects metrics and statistical data.__

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the __filebeat-config__ file to __ansible/Files__.
- Update the __config file__ to include __Elk Server Private IP__
- Run the playbook, and navigate to __Elk Public IP:5601/Kibana__ to check that the installation worked as expected.

- Which file is the playbook? __Filebeat-Playbook.yml__ Where do you copy it? __/etc/filebeat/filebeat.yml__

- Which file do you update to make Ansible run the playbook on a specific machine? __filebeats-config.yml__ 

- How do I specify which machine to install the ELK server on versus which to install Filebeat on? __You specify by updating the Hosts name on the Install-Elk.yml__

- Which URL do you navigate to in order to check that the ELK server is running? __http://40.78.1.88:5601/app/Kibana__

__**Here are the specific commands the user will need to run to download the playbook, update the files, etc.**__

 - ssh azureuser@JumpBoxPublicIP
 
 - ssh-keygen
 
 - curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > filebeat-configuration.yml
 
 - curl https://gist.githubusercontent.com/slape/58541585cc1886d2e26cd8be557ce04c/raw/0ce2c7e744c54513616966affb5e9d96f5e12f73/metricbeat > metricbeat-config.yml
 
 - sudo su
 - Docker start funny_borg
 - Docker attach funny_borg
 - nano filebeat-configuration.yml
 - nano metricbeat-config.yml
 - nano install-elk.yml
 - nano filebeat.yml
 - nano metricbeat.yml
 - ansible-playbook install-elk.yml
 - ansible-playbook filebeat.yml
 - ansible-playbook metricbeat.yml
