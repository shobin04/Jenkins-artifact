pipeline {
    agent any
    
    stages {
        stage('SCM checkot') {
            steps {
               git branch: 'main', url: 'https://github.com/shobin04/jenkins.git'
        }  
    }
    stage('Mvn build') {
        steps {
            script {
                sh """cd /var/lib/jenkins/workspace/Demo-Artifact/java-hello-world-with-maven-master
                mvn package"""
            }
        }
    } 
    stage('uploading artifact') {
        steps {
            script {
                withCredentials([[$class:'AmazonWebServicesCredentialsBinding', credentialsId:'s3-publish', accessKeyVariable:'AWS_ACCESS_KEY_ID', secretKeyVariable:'AWS_SECRET_ACCESS_KEY']]) {
                    sh"""
                    cd /var/lib/jenkins/workspace/Demo-Artifact/java-hello-world-with-maven-master/target
                    ls -ltr
                    aws s3 cp jb-hello-world-maven-0.2.0.jar s3://jenkins-artifact-demo-1"""
                    }
                }
            }
        }
    }
}
