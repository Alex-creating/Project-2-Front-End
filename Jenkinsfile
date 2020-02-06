pipeline {
    agent any
    stages {
        
        stage('---buildDocker---') {
        steps {
        sh "docker build -t alexr12/fronttest ."
        }
        }
                stage('---pushToDocker---') {
        steps {
        withDockerRegistry([ credentialsId: "DockerLog", url: "" ]) {
        sh "docker push alexr12/fronttest"
        }
        }
        }
       		       		stage('---SSH into test VM---') {
        		steps {
        		sh "ssh -T -i /home/ubuntu/DevOps.pem ubuntu@ec2-3-8-94-92.eu-west-2.compute.amazonaws.com ./script.sh"
        }}
        stage('---SSH into real VM---') {
        		steps {
        		sh "ssh -T -i /home/ubuntu/DevOps.pem ubuntu@3.10.150.209 ./script.sh"
        }}
    }
}
