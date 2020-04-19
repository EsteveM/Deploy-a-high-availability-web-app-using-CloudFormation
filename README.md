# Deploy a high-availability web app using CloudFormation

This project is intended to deploy an application (Apache Web Server). Code is picked up from S3 Storage and deployed in the appropriate folder on the web server. Firstly, a diagram is developed. Then, a matching CloudFormation script is created.

## Table of Contents

* [Description of the Project](#description-of-the-project)
* [Getting Started](#getting-started)
* [Contributing](#contributing)

## Description of the Project

As has already been mentioned, this project deploys an application (Apache Web Server) making use of an infrastructure as code script. The work that has been done is best described by explaining its main parts:

* A Launch Configuration for the application servers is created in order to deploy four servers, two located in each of the two private subnets. The launch configuration will be used by an auto-scaling group.
* An Instance size and Machine Image (AMI) are chosen to meet the specifications. These are two vCPUs, at least 4GB of RAM, and an Ubuntu 18 Operating System. 10GB of disk space are also allocated. 
* An IAM Role is created that allows the instances to use the S3 Service. As already mentioned, the application archive is downloaded from an S3 Bucket.
* The application communicates on the default HTTP Port: 80, so the servers need this inbound port open since it will be used by the Load Balancer and the Load Balancer Health Check. As for outbound, the servers need unrestricted Internet access to be able to download and update its software.
* The load balancer allows all public traffic (0.0.0.0/0) on port 80 inbound, which is the default HTTP port. Outbound, it will only be using port 80 to reach the internal servers.
* The application is deployed into private subnets with a Load Balancer located in a public subnet.
* One of the output exports of the CloudFormation script is the public URL of the LoadBalancer. http:// is added in front of the load balancer DNS Name in the output, for convenience.

## Getting Started

These are the steps followed to test the project accomplishes its goals:

* Firstly, you have to download/clone the project files from this repository onto your local machine. Then, cd into the root folder where the project files are located.
* Secondly, you can execute both cloudformation scripts. The first one includes the network part of the project, and the second one the servers part. For the former, type `./create.sh final-project-network final-project-network.yml final-project-network.json.` For the latter, type `./create.sh final-project-servers final-project-servers.yml final-project-servers.json`. This is the result of the execution of both scripts on the terminal:
![script1](/ScreenShots/script1.png)
![script2](/ScreenShots/script2.png)
And on the console:
![script3](/ScreenShots/script3.png)
* Thirdly, as an output of the *final-project-servers* script, we have a URL with the Load Balancer DNS Name and “http” in front of it:
![script4](/ScreenShots/script4.png)
* Finally, if we click on the URL to verify the work is running properly, a page is shown on the browser saying “It works! Udagram, Udacity”
![script5](/ScreenShots/script5.png)

## Contributing

This repository contains all the work that makes up the project. Individuals and I myself are encouraged to further improve this project. As a result, I will be more than happy to consider any pull requests.
