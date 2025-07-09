
# MarketPeak Ecommerce Website

The project is about E-commerce platform deployment using `version control`, `linux server administrative commands`, `AWS EC2 Instance`, and `Continuous Integration and deployment workflow`. A website template will be downloaded to start the development.

# Tasks

The following tasks will be performed for the complete deployment process:

1. Version control with Git
2. E-commerce website template download
3. Staging and commiting the template to Git
4. Pushing code to remote repository (Github)
5. Setting up an AWS EC2 instance
6. Cloning the repository on linux server
7. Web server installation
8. Continuous integration and deployment workflow


## Version Control with Git and Template Download

A project directory named `MarketPeak_Ecommerce` was created and initialized with the following commands:

```
mkdir MarketPeak_Ecommerce

cd MarketPeak_Ecommerce

git init

```
See the screenshot below:

![image](https://github.com/user-attachments/assets/aeaaf832-c5a7-43e6-a690-3a690ad7c219)

A Website template was downloaded from toolplate website. The downloaded file was extracted into the project directory

![image](https://github.com/user-attachments/assets/9650866e-caf7-46fc-b9ae-1e8a89977746)

The index file of the extracted template was opened in VS code for cutomization. The header was edited from `Waso Strategy` to `MarketPeak Ecommerce`

![image](https://github.com/user-attachments/assets/3a19cff8-45a7-48d1-a94c-6037f6c1f416)


![image](https://github.com/user-attachments/assets/8c1c9aea-999b-4210-b2c7-920afd3c7e2d)


The website files were added to Git repository using the following commands to add, stage and commit changes.

```
git add .
git status
git commit -m "Initial commit with basic e-commerce site structure

```
![image](https://github.com/user-attachments/assets/41c13e5e-e293-4454-8459-01a28ac30f5e)


![image](https://github.com/user-attachments/assets/53573115-b7d2-4bda-9ea3-89978b9e8a83)


## Pushing Code to Remote Repository (Github)

A new repository named `MarketPeak_Ecommerce` was created in Github without a README, .ignore or license.

![image](https://github.com/user-attachments/assets/348fc04e-24ee-4ec8-a002-7b2b3b3c2e86)

To link the local reposirory to the remote repository, the following command was used: `git remote add origin https://github.com/f-oni/MarketPeak_Ecommerce.git`.

![image](https://github.com/user-attachments/assets/bfa02a52-c39b-4101-86e1-0dd0246911c2)

In order to upload the content of the local repository to Github, the command `git push -u origin main` was used.

![image](https://github.com/user-attachments/assets/c8677c00-d805-49c6-93ca-74a159a4d862)


![image](https://github.com/user-attachments/assets/c163bbdc-1a7f-44de-b61f-2405536f6dfc)

## Setting Up an AWS EC2 Instance

An instance of t2.micro linux server was launched on AWS.

![image](https://github.com/user-attachments/assets/4500a93d-334e-4dba-8bd9-4812bc16ab88)

The EC2 instance was connected to, through **SSH** using MobaXterm. See the interface below

![image](https://github.com/user-attachments/assets/f8ff4c85-8eb9-4773-a24a-d60b9e1d8ed0)

## Cloning the Repository on Linux Server

To autheticate with github, a choice is to be made between **SSH** and **HTTPS**. The SSH method was chosen for this project. This required generating ssh keypair on the server and registering the public key in Github. On the EC2 instance linux server, a key pair was generated using the command `ssh-keygen` and a passphrase was also set for the key.

![image](https://github.com/user-attachments/assets/25c0d978-a6fa-4693-9429-c0a63199102a)

The public key was displayed with the command `cat /home/ubuntu/.ssh/id_ed25519.pub` and copied to the clipboard.

![image](https://github.com/user-attachments/assets/95cdaf1f-3238-4c5e-85a2-f3a531cb99c0)

The public key was added to Github by navigating to `seeting ==> SSH and GPG Keys ==> SSH` and a title, `web-server` was assigned. 

![image](https://github.com/user-attachments/assets/c1051273-47bb-4732-ae5e-577e5f3bf9b5)


![image](https://github.com/user-attachments/assets/7df2e6b3-4140-408e-9d4d-ea3410c5d1ce)

After the public key was succesfully registered on github, cloning the repository on the linux server, the following command was used `git@github.com:f-oni/MarketPeak_Ecommerce.git`

![image](https://github.com/user-attachments/assets/e8e09eaf-1349-40d1-b374-707a4a5f4050)

## Web Server Installation

A web server is used to serve `html` files and contents over the internet. The recommended Web server for the project is Apache Web server. To install it on the ubuntu server, the following commands were utilized:

```
sudo apt update
sudo apt install apache2

```

![image](https://github.com/user-attachments/assets/6a11f1fd-9d2e-49a9-9799-13ab6dc46c07)


![image](https://github.com/user-attachments/assets/d155baa5-f573-4347-9ebe-53916e6b2673)

To confirm Apache installation and status, the following command was used: `sudo systemctl status apache2`. The output showed that the service is enabled, active and running.

![image](https://github.com/user-attachments/assets/32ba7f8b-8560-4741-8eca-899720998d11)

## Web Server Configuration

The content of the default Apache web server directory, `/var/www/html` would have to be replaced with the content of the project directory. The following commands were used to first clear the content of the default directory before coppying over the content of MarketPeak_Wcommerce to it. 

```
sudo rm -rf /var/www/html/*
sudo cp -r ~/MarketPeak_Ecommerce/*  /var/www/html/
sudo systemctl reload apache2

```

![image](https://github.com/user-attachments/assets/5a7e7ebf-245d-428f-bb96-d5253c223d66)

## Accessing the website from a browser

The public ip address of the EC2 instance was entered into the address bar of a web browser to display the web content but the site was unreachable as shwon below:

![image](https://github.com/user-attachments/assets/2faf04fc-8aa7-4230-b7b2-0267c0743c96)

After some troubleshooting, it was discovered that inbound traffic to the server was blocked by default. to resolve the issue, a new security group rule was created to allow inbound traffic from **HTTP (port 80)** and **HTTPS (port 443)** and the rule was attached to the EC2 instance. The public IP address of the instance was again entered to the address bar of a browser and the website was successfully rendered.

![image](https://github.com/user-attachments/assets/d6bf7021-b2cd-4ce5-999b-12f94b3572f9)

## Continuous Integration and Deployment Workflow

This is meant to simulate making changes in a development environment and deploying update to production server.

A new branch named `development` was created and switched to using the following commands:

```
git branch development
git checkout development
 
```
![image](https://github.com/user-attachments/assets/31b74ee7-b3b4-47f9-9e7e-2ec46b42501d)

On the the development branch, the index file was updated with VS Code. The `ABOUT` section was updated by repurposing the title and content to align with **MarketPeak Ecommerce's**. The original version of the about section and the VS Code modification screenshots are shown below:

![image](https://github.com/user-attachments/assets/4f80a3bc-e8b2-4a13-8a08-383bbfc24498)


![image](https://github.com/user-attachments/assets/08d3db15-db21-4657-b888-7cbefae94f17)

The modification to the index file was saved in VS Code. The changes were added to the local repository for staging and and later committed to the development branch. The following commands were used:

```
git add .
git status
git commit -m "Modification to the ABOUT section"

```

![image](https://github.com/user-attachments/assets/bd0500ee-b85c-41fe-bba1-c771407e5240)

The committed changes were pushed to Github with the command: `git push origin development`

![image](https://github.com/user-attachments/assets/6b381c93-1ef3-41dd-87a0-0290db97191c)

The development branch was selected in github and a pull request was created to merge changes to the main branch.

![image](https://github.com/user-attachments/assets/2f8691ac-b305-4d07-a9e7-00b5fd9283f1)

There was no conflift between the main branch and the development branch, hence the development branch was merged with the main branch.

![image](https://github.com/user-attachments/assets/e19f7422-4125-45e4-8b9b-17d6e5c621f0)

On the local branch, the main branch was switched to from the development branch with the command `git checkout main`. The two branches were also merge with the command `git merge development`.

![image](https://github.com/user-attachments/assets/93d613ef-268c-4d32-9eea-2ad4f93354bc)

To properly synchronize the the local repository and the remote, the command `git pull origin main` was used

![image](https://github.com/user-attachments/assets/45190681-ae5f-458b-b300-15638d92121d)

The directory folder on the linux server was updated with the following commands:

```
cd MarketPeak_Ecommerce
git pull origin main

```

![image](https://github.com/user-attachments/assets/3a4a5a50-54c0-4164-8015-e3d94eea73cf)

Apache web server directory was updated and reloaded with the command `sudo systemctl reload apache2

![image](https://github.com/user-attachments/assets/f82d859c-40c1-4773-9eac-55f36b0efd5c)

The public ip address of the linux server was again copied to a browser and reloaded and the updated modification was reflected in the newly rendered page as shown below:

![image](https://github.com/user-attachments/assets/46b5b3c2-f389-4621-ae83-dec57fc504bc)

## Conclusion

The project successfully accomplished web site deploymet using version control, linux server, web server configuration, continuous integration and deployment workflow.


















































