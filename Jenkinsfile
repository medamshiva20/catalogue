pipeline{
    agent { node {label 'label1'} }
    stages{
        stage('Install Dependencies')
        {
            steps{
                sh 'npm install'
            }
        }
        stage('Unit Test')
        {
            steps{
                echo "Unit Testing is done here"
            }
        }
        stgae('Sonar Scanner')
        {
            steps{
                sh 'ls -ltr'
                sh 'sonar-scanner'
            }
        }
    }
}




// #!groovy
// //It means the libraries will be download and accessible at run time 
// @Library('roboshop-library') _

// def configMap = [
//     application: "nodeJSVM",
//     component: "catalogue"
// ]

// //This is .groovy file name and function inside it 
// pipelineDecission.decidePipeline(configMap)