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
       		       		stage('---SSH into VM---') {
        		steps {
        		sh "ssh -T -i /home/ubuntu/DevOps.pem ubuntu@ec2-13-8-94-92.eu-west-2.compute.amazonaws.com ./script.sh"
        }}
        
    }
}
