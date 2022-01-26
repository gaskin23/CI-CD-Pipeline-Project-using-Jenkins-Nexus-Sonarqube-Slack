# CI-CD-Pipeline-Project-using-Jenkins-Nexus-Sonarqube-Slack

## Description

This project aims to deploy Visual Profile Maven Project to Nexus repository with CI/CD Jenkins, Sonarqube, Nexus,GİT/Github,Slack and AWS EC2 instance.

## Tools is Used For This Project

![Project_Tools](./Project-Tools-1.png)
![Project_Tools_2](./Project-Tools-2.png)

## Scenario
You have a product development and agile SDLC is in motion, so a bunch of smart developers in an agile team will regularly make changes. So there'll be multiple code changes every day. And all this code needs to be tested because this is what actually is building your product. this code needs to be regularly built and tested. usually in an enterprise, there will be a separate building release team will be doing this job of building, testing and releasing the code, or if it's a small industry, then they'll be it will be developer's responsibility to merge and integrate this code.there are regular quote changes also called comments or pull requests, developers will be dependent on building the team, usually to test the code and move it to the next level in the release cycle. The code will be tested if there are any bugs or whether it will be known late due to these bugs and errors in the code. Keep accumulating and let's say these got accumulated. A problem goes much deeper now, developers need to rework to fix these bugs and errors, which is time consuming process and seems would be already approaching the deadline.

So solution to this problem is a regular build and test for every comet, so as soon as there is a code change, the code needs to be built and tested at the same time. if the process is manual, this will not be possible. you need to have an automated building release process. whenever there is a big and test of the court, the developers should get notified automatically. if you have such kind of automation framework in place, which will regularly build and test the code for every comic, then you're also removing dependency of developers from building steam. This process itself is called continuous integration process. So input to this process is any good comic and output will be well tested artifact and all this will happen automatically.
## Current Situation

![Project_CI/CD](./Project-Tools-1.png)
- Agile SDLC
- Developers make regular code changes
- These commits needs to be Build & Tested
- Usually Build & Release Team will do this Job
- Or Developers responsibility to merge an integrate code



  - Create a new public repository for the project on GitHub.

  - Create docker image using the `Dockerfile` from the base image of `python:alpine`.

  - Deploy the app on swarm using `docker compose`. To do so on the `Compose` file;

    - Create a MySQL database service with one replica using the image of `mysql:5.7`;

      - attach a named volume to persist the data of database server.

      - attach `init.sql` file to initialize the database using `configs`.

    - Configure the app service to;

      - pull the image of the app from the AWS ECR repository.

      - deploy the one app for each swarm nodes using `global` mode.

      - run the app on `port 80`.

    - Use a user-defined overlay network for the services.

  - Push the necessary files for your project from local repo to the new github repo (phonebookswarm).

- You are also requested; to use AWS ECR as image repository, to create Docker Swarm with 3 manager and 2 worker node instances, to automate the process of Docker Swarm initialization through Terraform in the development environment. To achieve this goals, you can configure Terraform configuration file using the followings;

  - The application should run on Amazon Linux 2 EC2 Instance

  - EC2 Instance type can be configured as `t2.micro`.

  - To use the AWS ECR as image repository;

    - Enable the swarm node instances with IAM Role allowing them to work with ECR repos using the instance profile.

    - Install AWS CLI `Version 2` on swarm node instances to use `aws ecr` commands.

  - To automate the process of Docker Swarm initialization;

    - Install the docker and docker-compose on all nodes (instances) using the `user-data` bash script.

    - Create the leader manager node of the swarm. Within the `user-data` script;

      - Set the first manager node hostname as `Leader-Manager`.

      - Initialize Docker swarm.

      - Create a docker service named `viz` on the manager node on port `8080` using the `dockersamples/visualizer` image, to monitor the swarm nodes easily.

      - Build the docker image from the GitHub URL of the new project repo and tag it appropriately to push it on ECR repo. (Note: Do not forget to install Git to enable Docker to work with git commands)

      - Download `docker-compose.yml` file from the repo and deploy application stack on Docker Swarm.

    - Create two manager nodes of the swarm. Within the `user-data` script;

      - Install the python `ec2instanceconnectcli` package for `mssh` command.

      - Connect from manager node to the `Leader-Manager` to get the `join-token` and join the swarm as manager node using `mssh` command.
    
    - Create two worker nodes of the swarm. Within the `user-data` script;

      - Install the python `ec2instanceconnectcli` package to use `mssh` command.

      - Connect from worker node to the `Leader-Manager` to get the `join-token` and join the swarm as worker node using `mssh` command.

  - Create a security group for all swarm nodes and open necessary ports for the app and swarm services.

  - Create an image repository on ECR for the app.

  - Tag the swarm node instances appropriately as `Docker-Swarm-Manager  <Number>/Docker-Swarm-Worker <Number>` to discern them from AWS Management Console.

  - The Web Application should be accessible via web browser from anywhere.

  - Phonebook App Website URL, Visualization App Website URL should be given as output by Cloudformation Service, after the stack created.

## Project Skeleton

```text
204-docker-swarm-deployment-of-phonebook-app-on-python-flask-mysql (folder)
|
|----readme.md            # Given to the students (Definition of the project)
|----cfn-template.yml     # To be delivered by students (Cloudformation template-Optional)
|----phonebook-app.py     # Given to the students (Python Flask Web Application)
|----requirements.txt     # Given to the students (List of Flask Modules/Packages)
|----init.sql             # Given to the students (SQL statements to initialize db)
|----main.tf              # To be delivered by students (Terraform configuration file)
|----Dockerfile           # To be delivered by students
|----docker-compose.yml   # To be delivered by students
|----templates
        |----index.html      # Given to the students (HTML template)
        |----add-update.html # Given to the students (HTML template)
        |----delete.html     # Given to the students (HTML template)
```

## Expected Outcome

![Phonebook App Search Page](./search-snapshot.png)

### At the end of the project, following topics are to be covered;

- Docker Swarm Deployment

- Web App and MySQL Database Configuration in Docker Swarm

- Bash scripting

- AWS ECR as Image Repository

- AWS IAM Policy and Role Configuration

- AWS EC2 Configuration

- AWS EC2 Security Group Configuration

- Terraform Configuration File

- Git & Github for Version Control System

### At the end of the project, students will be able to;

- demonstrate how to configure Dockerfile and docker-compose files.

- set up a Docker Swarm cluster to work with AWS ECR using Terraform.

- deploy an application stack on Docker Swarm.

- create and configure AWS ECR from the AWS CLI.

- use Docker commands effectively to tag, push, and pull images to/from ECR.

- demonstrate bash scripting skills using `user data` section in Terraform to install and setup Docker and application environment on EC2 Instances.

- demonstrate their configuration skills of AWS EC2, IAM Policy, Role, Instance Profile, and Security Group.

- configure Terraform template to use AWS Resources.

- apply git commands (push, pull, commit, add etc.) and Github as Version Control System.

## Resources

- [AWS CLI Command Reference](https://docs.aws.amazon.com/cli/latest/index.html)

- [Docker Compose File Reference](https://docs.docker.com/compose/compose-file/)

- [Docker Reference Page](https://docs.docker.com/reference/)

- [EC2 Instance Connect](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Connect-using-EC2-Instance-Connect.html)
