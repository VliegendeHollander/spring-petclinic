pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                step(
                    checkout([$class: 'GitSCM', 
                    branches: [[name: 'main']], 
                    doGenerateSubmoduleConfigurations: false, 
                    extensions: [], 
                    submoduleCfg: [], 
                    userRemoteConfigs: 
                    [[credentialsId: 'dd67f719-59b1-4e47-a9fa-67b6ee7f6938', 
                    url: 'https://github.com/VliegendeHollander/spring-petclinic.git']]
                    ])
                );
                // step(
                //     copyArtifacts fingerprintArtifacts: true, 
                //     projectName: 'PollsSCM', 
                //     selector: lastSuccessful(), 
                //     target: '/var/www'
                // )

                sh "rm -rf /var/www/target"

                sh "mvn clean install -DskipTests"
        
                // step(
                // // echo "Copy artifact..."
                //     [$class: 'CopyArtifact',
                //         projectName: 'PollsSCM',
                //         target: '/var/www']
                // )
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