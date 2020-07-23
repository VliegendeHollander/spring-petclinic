pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // step(
                //     checkout([$class: 'GitSCM', 
                //     branches: [[name: 'main']], 
                //     doGenerateSubmoduleConfigurations: false, 
                //     extensions: [], 
                //     submoduleCfg: [], 
                //     userRemoteConfigs: 
                //     [[credentialsId: 'dd67f719-59b1-4e47-a9fa-67b6ee7f6938', 
                //     url: 'https://github.com/VliegendeHollander/spring-petclinic.git']]
                //     ])
                // );
                // step(
                //     copyArtifacts fingerprintArtifacts: true, 
                //     projectName: 'PollsSCM', 
                //     selector: lastSuccessful(), 
                //     target: '/var/www'
                // )
                step(
                    // echo "Deleting target repository..."
                    sh 'rm -rf /var/www/target/'
                );

                step(
                    // echo "Building the project..."
                    mvn clean install
                );
        
                step(
                // echo "Copy artifact..."
                    [$class: 'CopyArtifact',
                        projectName: 'PollsSCM',
                        target: '/var/www']
                );
            }
        }
       
        stage('Deploy') {
            steps {
                sh 'mv /var/www/target/spring-petclinic-*.jar /var/www/target/spring-petclinic-prod.jar'
                sh 'sudo systemctl restart petclinic'
            }
        }
    }
}