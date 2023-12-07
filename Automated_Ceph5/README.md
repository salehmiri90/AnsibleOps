
# Automated_Ceph_Deployment
A real world scenario codes to automate your infrastructure to build Ceph 5 or Ceph 6 clusters.

# Use this codes to install "Ceph 5"
At the very first step, please find "ks.cfg" file for deploy it as kickstart file and use it to install server's operating system (redhat) in minimum time.
There are some solutions for baremetal provisioning include  kickstart,foreman, MaaS,etc. It's depends on your preference.

I try to put comments in each file to help you when use the playbook.
You need to run playbooks in order. 
In below, I explained each playbooks. Please consider that this repo is updating continiously.

00-hostname.yaml:
in your ansible playbook directory, need to create a folder called host_vars and set the name of that exactly same as you defined in ansible /etc/hosts file.
the first block use host_vars content to set hostName. the next block change interface configuration to enable onboot and disable ipv6.
at the end, will restart network.

01-katello.yaml:

This file is check the target server IP and DNS addreesses and display it during playbook run to ensure you are working in correct machines and your machines can reach the dns servers.
after that the katelo rpm will install. this rpm located in httpd web service and the "katello_url" exists as a variable in group_vars/all.
in the next task, your target server will be subscribe to redhat using "org_id" and "activationkey" which exists as a variable in group_vars/all.
To check your subscription run correctly, the command of "yum repolist" run and output will shown after playbook runs.


02-rpm.yaml:

This file is installing required packages to prepare server's environment. the packages list exist in group_vars/all.


03-chrony.yaml:

As the name demonstrate, this playbook checks configuration related to time then restart the service.
if you have multiple clusters, by using "when" module and based on gateway address which ansible find our from facts, determined which parameter need to set for ntp.
the ntp ip addresses exist in group_vars/all.


04-bond.yaml:

If your cluster is using a private (interconnect) interfaces for within cluster communications, so you need to run this playbook to configure bond in your servers.


05-registry.yaml:

I used a custome url for my image repository (nexus, artifactory), thus I copy the configuration file from ansible machine to target server with required permissions.
In next task, the zabbix agent copy to target machine and run it as container. After that, podman will used to pull and tag my containers.


06-adm.yaml:

This config file only need to run on your cephadm machine which always called MON1. 
The cephadm package is installed then transfer my customized cephadm configuration from ansible machine to target server with required permissions.
After that due to add osds on MON1 after bootstrap, I copied required files to MON1.
At the end, configuring smtp to send alerts.


07-mons.yaml:

For configuring ceph mons, you need to copy keyrings from mon1 to other mons, so you need to run this playbook to do that. the files permission is mandatory.
After that, using podman to pull and tag required images, you can find the images name and tags in group_vars/all.


08-ceph-ssh-copy.yaml:

Same as previous step, due to connect mon1 to other mons by password-less ceph user, you need to copy ceph.pub to other mons by running this playbook.


09-checkDisk.yaml:

On your osd servers and due to required configurations, you need to check the disks be in order then running pv,vg,lv commands to build your osd infra, so running this playbook to have a detail look on your osds.


10-configDisk.yaml:

After you checked the physical disk on osd servers, you need to configure pv,vg and lv based on parmeters you set in host_vars/hostname. this file will import later in this repo.


11-add-host.yaml:

After your osds are ready, you can run this playbook on mon1 to add hosts with physical disks into your ceph cluster. the variables load from host_vars file.


12-xoroux.yaml:

Except our zabbix monitoring, I use xoroux company software for our physical server's monitoring by agent and this playbook run configuration related to this subject.


13-pmp.yaml:

If you have pmp for increase security policy on your cluster's environmnt, you can put configuration file into ansible machine, then ansible transfer and run in target.


14-userlock.yaml:

Based on security policy, it's highly recommended after your cluster run and fine, disable ansible user from cluster's servers and remove it's authority to be sudeor. this playbook do both.
After running this task, you'll not be able to connect from ansible machine to target servers. 

### 🎥 Video Demo on Youtube
Instruction video is already uploaded to my youtube channel [salehmiri90](https://youtube.com/salehmiri90) and the video names are:

&#9745; 

## ✍ Contribution
I am confident that working together with skilled individuals like yourself can improve the functionality, efficiency, and overall quality of our projects. Therefore, I would be delighted to see any forks from this project. Please feel free to use this code and share any innovative ideas to enhance it further.

## ☎ Contact information
#### 📧 salehmiri90@gmail.com
#### [Linkedin.com/in/salehmiri](https://www.linkedin.com/in/salehmiri)
