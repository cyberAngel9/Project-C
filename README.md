# Project-C
Project on azure cloud
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://drive.google.com/file/d/1meCX_8mtN2Z5CDl7kfVe-x27poVyMn4d/view?usp=sharing

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._
---
- name: My first playbook
  hosts: webservers
  become: true
  tasks:
   - name: docker.io
      apt:
        update_cache: yes
        name: docker.io
        state: present

    - name: Install pip3
      apt:
        name: python3-pip
        state: present

    - name: Install python Docker module
      pip:
        name: docker
        state: present

    - name: Downloand and launch a docker web container
      docker_container:
        name: dvwa
        image: cyberxsecurity/dvwa
        state: started
        restart_policy: always
        published_port:80:80

     - name: Enable docker service
       systemd:
         name: docker
         enabled: yes



This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive, in addition to restricting in bound access to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?
 If a DDos attack accure to the vm the load balancer will divied the attcking traffic across the network. For users to access the jump box from one access point and monitored.  

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the jump box and system network.
- _TODO: What does Filebeat watch for? Any changes to the files in the machines. 
- _TODO: What does Metricbeat record? Records or collects any metrics from the servers that are running and from the operating system. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
|ELK VM    |Monitoring| 10.2.0.4   | Linux            |
| Web 1    |Web Server| 10.0.0.7   | Linux            |
| Web 2    |Web Server| 10.0.0.9   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses Kibabna port 5061

Machines within the network can only be accessed by Jump box.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_ 52.255.205.91 Jump Box

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |  10.0.0.4            |
| Web 1    | No                  |  10.0.0.7            |
| Web 2    | No                  |  10.0.0.9            |
  Elk VM     No                     10.2.0.4

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
 Ansible is an open source tool and thier are diffrent ways to set up or conigure a playbook.
The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install docker
- Install pip3
- Install python docker module
- Download and launch a docker web container
- Enable docker service

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output] https://drive.google.com/file/d/1meCX_8mtN2Z5CDl7kfVe-x27poVyMn4d/view?usp=sharing

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
 Web 1 10.0.0.4
 Web 2 10.0.0.9
We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
 Microbeats

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
 Filebeat collects data about the system file and Metricbeat collectsmachine metrics.
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk instal.yml file to elk install.yml.
- Update the elk install.yml file to include...
- Run the playbook, and navigate to http://52.175.200.75:5601/app/kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_ Filebeat-playbook.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? Install-elk.yml Configure Elk VM with Docker

- _Which URL do you navigate to in order to check that the ELK server is running? http://52.175.200.75:5601/app/kibana

