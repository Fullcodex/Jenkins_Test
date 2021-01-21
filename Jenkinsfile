pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'javac src/jenkins_test/Jenkins_Test.java'
                sh 'cd src && java jenkins_test.Jenkins_Test'
                sh './src/jenkins_test/Jenkins_Test build'
            }
        }
        stage('Test') {
            steps {
                //sh 'chmod 777 unitTests.xml'
                junit 'unitTests.xml'
            }
        }
        stage('Deploy') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
                sh 'make publish'
            }
        }
    }
}
