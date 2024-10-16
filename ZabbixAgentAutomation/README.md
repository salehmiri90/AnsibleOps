# Zabbix Agent Ansible Role

## Overview

I recently developed a lightweight Ansible role designed to install and configure Zabbix agents across multiple servers. Below is a guide on how to utilize this role effectively.

## Module Usage

This Ansible role leverages various modules, ensuring that each one is used efficiently and without redundancy on the target nodes. By employing these modules multiple times, we avoid duplication and maintain cleaner configurations.

## Key Tasks

The primary tasks are defined in zabbix-agent.yml, which begins by gathering facts about the target servers. This information is then utilized in two specific roles:

1. Offline Repository Role: Located in roles/offline-repo/, this role adds the appropriate Zabbix repository URLs based on the gateway IP address of the defined nodes.

2. Zabbix Agent Role: This role is responsible for installing and configuring the Zabbix agent for production use.

## Role Details

Offline Repository Role
In the offline-repo role, we utilize Ansible facts to determine the gateway IP address of each node. Based on this information, we add the suitable repository for Zabbix.

## Zabbix Agent Role

Within the Zabbix-agent role, the necessary packages are installed, and the service is enabled. The configuration process includes setting up the Zabbix proxy for each site using the respective node's gateway IP address. Additionally, the hostname from each node is used to configure zabbix-agent.conf. Finally, the Zabbix agent is restarted to apply all changes.

## Start to Use this code
### Step 1: Transfer codes to your Server
&#9745; To clone this repository from my GitHub using the command line, you can use the following command:
````
git clone https://github.com/salehmiri90/Ansible-Projects.git
````

&#9745; Use the 'cd' command to get into the contents of the cloned directory 'Ansible-Projects' and this project realted directory 'zabbix-agent-conf' as follows: 
````
cd Ansible-Projects/zabbix-agent-conf
````

&#9745; And then listing the contents with the command: 
````
ll
````

### Step 2: Defining Variables
&#9745; Modify below files and set the correct variables based on your infrastracture and environment.
````
vim hosts
````
&#9745; Modify the `path`, `baseurl` and gateway ip addresses in the below file.
````
vim roles/offline-repo/main.yml
````
&#9745; Modify `Server=` , `ServerActive=` and gateway ip addresses in the below file.
````
vim roles/zabbix-agent/tasks/main.yml
````

### Step 3: Execution
&#9745; Check ansible connectivity to targets. the name of server group is 'miri'.
```
ansible server -i hosts -m ping
```

&#9745; Run the main playbook
```
ansible-playbook zabbix-agent.yml -i hosts
```

# ✍ Contribution
I am confident that working together with skilled individuals like yourself can improve the functionality, efficiency, and overall quality of our projects. Therefore, I would be delighted to see any forks from this project. Please feel free to use this code and share any innovative ideas to enhance it further.

## ☎ Contact information
#### 📧 salehmiri90@gmail.com
#### [Linkedin.com/in/salehmiri](https://www.linkedin.com/in/salehmiri)
