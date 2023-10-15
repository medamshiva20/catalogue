pipeline {
    agent { node { label 'AGENT-1' } }
    stages{
        stage('Get Version'){
            steps{
                script{
                    def packageJson = readJSON file: 'package.json'
                    def packageVersion = packageJSON.version
                    echo "${packageJSONVersion}"
                }
            }
        }
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
        stage('Build')
        {
            steps{
                sh '''
                ls -ltrh
                zip -r catalogue.zip ./* --exclude=.git --exclude=.zip
                '''
            }
        }
        stage('Publish Artifact')
        {
            steps{
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '172.31.34.61:8081/',
                    groupId: 'com.roboshop',
                    version: '1.0.2',
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
                echo "Deploy to production"
            }
        }
    }
        post{
            always{
                echo 'cleaning up workspace'
                deleteDir()
            }
        }
}