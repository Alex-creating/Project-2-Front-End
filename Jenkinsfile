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
        
    }
}