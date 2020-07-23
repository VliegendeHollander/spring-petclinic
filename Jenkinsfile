pipeline {
    agent any

    stages {
        stage('Build') {
            steps {

                echo "Deleting target directory..."
                sh "rm -rf /var/www/target"

                echo "Execute mvn clean install..."
                sh "mvn clean install -DskipTests"
        
                echo "Copy artifact..."
                step(
                    [$class: 'CopyArtifact',
                        projectName: 'PollsSCM',
                        target: '/var/www']
                )
            }
        }
       
        stage('Deploy') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    input message: "Do you want send the jar to production?"
                }
                    sh 'mv /var/www/target/spring-petclinic-*.jar /var/www/target/spring-petclinic.jar'
                    sh 'sudo systemctl restart petclinic'
            }
        }
    }
}