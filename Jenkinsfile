pipeline {
    agent any

    stages {
        stage('Build') {
            sh 'rm -rf /var/www/target' 
            steps {
                step ([$class: 'CopyArtifact',
                        projectName: 'spring-petclinic',
                        filter: 'spring-petclinic-*.jar',
                        target: '/var/www/target']);
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