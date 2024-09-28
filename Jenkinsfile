pipeline{
    agent { node {label 'agent-1'} }
    stages{
        stage('install dependencies')
        {
            steps{
               sh 'npm install'
            }
        }
        stage('Unit test')
        {
            steps{
                echo "Unit testing is done here"
            }
        }
        stage('Sonar scan'){
            steps{
                sh 'ls -ltr'
                sh 'sonar-scanner'
            }
        }
        stage('Build')
        {
            steps{
                echo "Building is done here"
                sh 'ls -ltr'
                sh 'zip -r catalogue.zip ./*  --exclude=.git --exclude=.zip'
            }
        }
        stage('Publish Artifact')
        {
            steps{
                    nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        nexusUrl: '172.31.80.163:8081',
                        groupId: 'com.roboshop',
                        version: '1.0.1',
                        repository: 'catalogue',
                        credentialsId: 'nexus-auth',
                        artifacts: [
                            [artifactId: 'catalogue',
                            classifier: '',
                            file: 'catalogue.zip',
                            type: 'zip']
                        ]
                    )
                }
        }
        stage('Deploy')
        {
            steps{
                echo "Deployment"
            }
        }
    }
    post{
        always{
            echo "deleting workspace"
            deleteDir()
        }
    }
}