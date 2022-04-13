## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

-Images/elkdiagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

- The file to download and set up metricbeat and file beat: Images/playbook.png

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient and the network load will be evenly distributed. In addition the load balancer restricts unfettered access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes made to log files and other specified location, as well as system performance.


The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.5   | Linux            |
| Elk-VM   | Elkstack | 10.1.0.4   | Linux            |
| Web-1    | Web VM   | 10.0.0.6   | Linux            |
| Web-2    | Web VM   | 10.0.0.7   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the ELK Stack machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Any IP address can ssh into the Elk Stack, but only the computer at my public IP at 23.246.116.5 is given access to port 5601.

Machines within the network can only be accessed by the jump box.
- Access was provided to my personal computer at the Public IP Address: 23.246.116.5

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |     No              | 23.246.116.5         |
| Web-1    |     No              | 10.0.0.5  10.1.0.4   |
| Web-2    |     No              | 10.0.0.5  10.1.0.4   |
| Elk-VM   |     Yes             | 23.246.116.5         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is beneficial, since ansible playbooks
can be run over many different machines, enabling users to spin up configured machines that are all exactly configured.

The playbook implements the following tasks:
- The first step is to download docker.io, and install python3-pip and the docker.
- Next we must increase the memory in the virtual machine to give enough room to create
  our elk stack.
- Lastly we have to download and launch the docker elk container, and make sure that the
  docker service will run on startup.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Images/docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.6 and 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat allows users monitor changes made in the log files. For example, if a very rude
  person was to write a script that would repeatedtly attempt to ssh into one of the
  in-network machines, Filebeat would log that data and you could see the data from that
  instance. It also provides a handy graphical interface to monitor the log files over time,
  or even streaming them live.
- Metricbeat collects information on system metrics. For example, filebeat is able to
  monitor the percentage of cpu usage on a machine. In this project, this is easily
  accomplished by running the stress command on one of the monitored machines

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the Images/filebeat-playbook.yml file to /etc/ansible/files.
- Update the hosts file to include the private IP addresses of the machines you want to
  run the playbook on.
- Run the playbook, and navigate to http://<ELK.VM.External.IP>:5601/app/kibana to check that the installation worked as expected. In our case the URL would be http://13.82.139.122:5601/app/kibana
