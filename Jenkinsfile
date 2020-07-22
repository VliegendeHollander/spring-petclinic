pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'rm -rf /var/www/target' 
                copyArtifacts(projectName: 'petclinic');
            }
        }
        stage('Test') {
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