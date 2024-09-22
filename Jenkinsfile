pipeline{
    agent { node {label 'agent-1'} }
    stages{
        stage('install dependencies')
        {
            steps{
                sh '''
                npm install
                '''
            }
        }
        stage('Unit test')
        {
            steps{
                echo "Unit testing is done here"
            }
        }
    }
}