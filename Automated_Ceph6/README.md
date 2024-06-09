# Deploying Ceph 6 with Automation Tools 
## Description
This repository will help you to do installation and configuration Ceph 6 on Redhat operating system version 8.  

## 🎥 Video Demo on Youtube

Instruction video is already uploaded to my youtube channel [salehmiri90](https://youtube.com/salehmiri90) and the video names are:

&#9745; In future will be published!

## Technologies and Tools
To implement this project, I only used Terraform and VMware vCenter product iso file. This method tested with vCenter 8.  

✅ `Ansible`

✅ `Ceph 6`

## Start to Use this code
### Step 1: Transfer codes to your Server
&#9745; To clone this repository from my GitHub using the command line, you can use the following command:
````
git clone https://github.com/salehmiri90/Automated_Ceph_Deployment.git
````

&#9745; Use the 'cd' command to get into the contents of the cloned directory 'Automated_Ceph_Deployment' and this project realted directory 'Automated_Ceph6' as follows: 
````
cd Automated_Ceph_Deployment/Automated_Ceph6
````

&#9745; And then listing the contents with the command: 
````
ll
````

### Step 2: Defining Variables
&#9745; Modify below files and set the correct variables based on your infrastracture and environment. Also you can configure general variables in 'group_vars/all.yml' file.
````
vim Automated_Ceph6/inventory/hosts
````

&#9745; Creat a copy from group variable templates file to a new file based on your group defination.
````
cp Automated_Ceph6/inventory/group_vars/template.yml Automated_Ceph6/inventory/group_vars/newgroup.yml
````
````
vim Automated_Ceph6/inventory/group_vars/newgroup.yml
````

&#9745; Creat a copy from host variable templates file to a new file based on your host defination.
````
cp Automated_Ceph6/inventory/host_vars/template.yml Automated_Ceph6/inventory/host_vars/newhost.yml
````
````
vim Automated_Ceph6/inventory/host_vars/newhost.yml
````

&#9745; 

### Step 3: Execution
&#9745; Format and Validate codes to download required providers
```
terraform fmt
terraform validate
```

&#9745; Check the changes before impact on infrastructure.
```
terraform plan
```
&#9745; Execute below Terraform command to double check plan then hit `yes` to make changes. 
```
terraform apply
```

# ✍ Contribution
I am confident that working together with skilled individuals like yourself can improve the functionality, efficiency, and overall quality of our projects. Therefore, I would be delighted to see any forks from this project. Please feel free to use this code and share any innovative ideas to enhance it further.

## ☎ Contact information
#### 📧 salehmiri90@gmail.com
#### [Linkedin.com/in/salehmiri](https://www.linkedin.com/in/salehmiri)
