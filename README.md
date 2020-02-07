# DevOps Project

The aim of this project was to create a fully-deployed version of a full-stack OOP application as a team of two. 

## Index

[Requirements](#requirements)

[Solution](#solution)

[Pipeline Architecture](#architecture)

[Testing](#testing)
* [Surefire Report](#surefire)

[Deployment](#deployment)
* [Technology used](#technology)

[Security](#security)

[Future Possibilities](#future)

[Authors](#author)

<a name="requirements"></a>
## Requirements

To create a fully-deployed version of a full stack OOP application, with the support of tools such as Jenkins, Docker, Nginx, Nexus and AWS. There should also be use of VPCs and subnets with appropriate security settings. Upon passing unit and integration tests, the application will be deployed through a test environment and onto a live environment.

<a name="solution"></a>
### Solution

Our team created a Jenkins pipeline which would test and run the development branch of our Git repository whenever a change was detected. Jenkins would also be sending an image of the current application to both Docker Hub and Nexus. Upon passing unit, integration and selenium tests the changes to the dev Branch would be pulled into the master branch. This change would again be detected by Jenkins and begin another pipeline to test it and deploy it into a live environment for the user to use.

<a name="architecture"></a>
## Pipeline Architecture

![pipeline](https://i.imgur.com/gNwsccQ.jpg) 

The above diagram shows the pipeline used to deliver continuous integration. Any changes in the source code are pushed to the dev branch on GitHub. A webhook from Jenkins pulls in the changed project and begins the pipeline as determined by the Jenkinsfile. Jenkins will test the unit and integration tests with a combination of JUnit and Mockito tests, then run mvn package and deploy, storing it in Nexus. Jenkins will SSH into an EC2 instance for the front and backend and run a pre-made script. This script pulls down the latest image from Docker Hub and runs it on a test environment. Selenium tests will run, upon them passing the application will be deployed to the live environment. 

![jenkins](https://i.imgur.com/SMuboRC.jpg)


<a name="testing"></a>
## Testing

Testing of this program included using JUnit, Selenium and Mockito, along with SonarQube to help idenfity and remove code smells to aid refactoring.

![junit](https://i.imgur.com/Q9ym4cZ.png)

<a name="surefire"></a>
### Surefire Report

[Surefire Report](./Surefire.pdf)

Test coverage from JUnit testing on Eclipse is 85%, SonarQube line coverage is at 82%, with 0 bugs, vunerabilities or code smells.

<a name="deployment"></a>
## Deployment 

Jenkins was used to build, test and deploy my project. Upon every push to my Git repository Jenkins would automatically begin this process and update my project. The application has been deployed using an Amazon Web Service (AWS) virtual machine (VM).

<a name=”security”></a>
## Security

When working with AWS, the master user account was never used, only an IAM user, with least privileges. Jenkins had a store of Docker Hub credentials such that no one would be able to access Docker and the password can’t be seen anywhere. 

No password were used in scripts as this is insecure. The database can only be accessed by the backend, there is no unnecessary access from other parts of the application.

![security](https://i.imgur.com/rGTWkKS.png)

<a name="technology"></a>
### Technology used

H2 Database - Database,
Java - Source Code,
Jenkins - CI Server,
Maven - Dependency Management,
JUnit, Selenium, SonarQube - Testing,
Surefire - Test Report,
Nexus and Docker Hub – Image Storage,
GitHub - Version Control System,
Trello - Project Tracking,
Amazon Web Service - Live Environment


<a name="future"></a>
## Future Possibilities

Add further security features such as not hard-coding the database login details in the application properties. The backend should be closed off on all port except by Jenkins when it comes to SSH, and should only be able to talk to the frontend and the database.

<a name="author"></a>
## Authors
Alexander Russo,
Zohaib Zahid

