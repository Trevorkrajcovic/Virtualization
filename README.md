# Virtualization
Project Files
## Automated ELK Stack Deployment

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
- Load balancers protect the data, if data is unavailable it can cause issues. 
- We implemented a Jump Box to serve as a platform to run our Containers, Dockers, VM's, Network Security Groups, etc. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system processors.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Windows          |
| Web 1    | Docker   | 10.0.0.5   | Windows          |
| Web 2    | Docker   | 10.0.0.6   | Windows          |
| Web 3    | Docker   | 10.0.0.8   | Windows          |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the virtual machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
71.205.147.6

Machines within the network can only be accessed by the host machine.

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because
the ansible container can take a playbook and make it run across all three of our Web virtual machines. This makes automation quick and
simple.

The playbook implements the following tasks:
- You first need to create a group called [elk] within your /etc/ansible/hosts file. Once you edit that file and add the group you create a playbook
to configure it. You then need to create the playbook, within the playbook you should have commands to install docker.io, python3-pip, and the 
actual docker container called sebp/elk:761. Once you have created the playbook, you run it in your terminal, and Elk should be installed at this 
point.

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web VM 1 [10.0.0.5] Web VM 2 [10.0.0.6] Web VM [10.0.0.8]

We have installed the following Beats on these machines:
- MetricBeat, and Filebeat

These Beats allow us to collect the following information from each machine:
- Filebeat: Collects data about the file system, extremely useful when using multiple VM's as Filebeat can collect logs from multiple machines.
- Metricbeat: Collects machine metrics, such as memory. It also gives us the ability to analyze system CPU.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Filebeat from the github file to /etc/ansible/files/filebeat-config.yml. You can accomplish this using the 'Curl' command.
- Update the filebeat-config.yml file to include the Ip address of each virtual machine, ex. 
- Run the playbook, and navigate to the ELK server DEB page to check status and to check that the installation worked as expected.

- The playbook is within the Ansible container located in /etc/ansible/ within the ansible container. The playbook is copied to /etc/ansible/files
- The config.yml file needs to be updated in order for the playbook to run. To specify the machine you're installing for instance filebeat, 
you would set the IP address in the config file to the machine you want it to run on. In my case I used the Web VM's and therefor specified their Ip's
- The URL to use to be sure your ELK Stack is running is as follows: http://[your.VM.IP]:5601/app/kibana.
