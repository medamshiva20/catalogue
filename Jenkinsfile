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
                sh 'zip -r ./* artifact.zip --exclude=.git'
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