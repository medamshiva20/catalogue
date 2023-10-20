pipeline {
    agent { node { label 'AGENT-1' } }
    environment{
        packageVersion = ''
    }
    stages{
        stage('Git Version')
        {
            steps{
                script{
                    def packageJson = readJSON(file: 'package.json')
                    packageVersion = packageJson.version
                    echo "version: ${packageVersion}"
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
                echo "Sonar scan done"
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
         stage('SAST')
        {
            steps{
                echo "SAST done here"
                echo "version: $packageVersion"
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
                    version: "$packageVersion",
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
        //Here I need to configure downstream job. I have to pass package version for deployment
        stage('Deploy')
        {
            steps{
                script
                {
                    echo "Deployment"
                        def params = [
                            string(name: 'version', value: "$packageVersion")
                        ]
                        build job: "../catalogue-deploy", wait: true, parameters: params
                }
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