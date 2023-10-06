pipeline {
    agent { node { label 'agent1' } }
    stages{
        stage('Install dependencies')
        {
            steps{
                sh '''

                npm install

                '''
            }
        }
        stage('Unit Test')
        {
            steps{
                echo "Unit testing is done here"
            }
        }
        //sonar-scanner command expect sonar-project.properties should be available
        stage('Sonar Scan')
        {
            steps{
                sh '''
                ls -ltr
                sonar-scanner
                '''
            }
        }
    }
}