# Dockerisation of Project

1. On AWS, create an EC2 instance and SSH into the instance. Clone the backend of the project:
- git clone https://github.com/Alex-creating/Project-1-Recipe-Store-.git


2. Download docker onto the instance:
- sudo snap install docker


3. Create an image of the backend:
- sudo docker build -t recipe .


4. Run the image as a container, stating that it should always restart:
- docker run --restart=always --name recipes-lol -d -p 9091:8080 recipe:latest
This can be tested by resetting the instance and seeing if the application starts up by itself.


5. Create an image of the finished backend instance (AMI) as well as a Target Group with the specified ports. Then create an auto scaling group together with a load balancer which attaches to the auto scaling group.


6. Repeat this process with the frontend, creating an instance, creating the image and running an always restarting container:
- docker run --restart=always --name frontend -d -p 9090:80 frontend


7. Create an image of the frontend instance, attach a load balancer to the auto scaling group and point the nginx on the frontend towards the backend load balancer.
