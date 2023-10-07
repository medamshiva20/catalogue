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
        // stage('Sonar Scan')
        // {
        //     steps{
        //         sh '''
        //         ls -ltr
        //         sonar-scanner
        //         '''
        //     }
        // }
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
                    nexusUrl: '172.31.81.122:8081/',
                    groupId: 'com.roboshop',
                    version: '1.0.0',
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
    }
        post{
            always{
                echo 'cleaning up workspace'
                deleteDir()
            }
        }
}