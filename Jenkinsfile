pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                step ([$class: 'CopyArtifact',
                        projectName: 'petclinic',
                        target: '/var/www']);
            }
        }
       
        stage('Deploy') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
                sh 'mv /var/www/target/spring-petclinic-*.jar /var/www/target/spring-petclinic-prod.jar'
                sh 'sudo systemctl restart petclinic'
            }
        }
    }
}