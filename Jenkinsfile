pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                //sh 'help'
                archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
                //sh 'javac src/jenkins_test/Jenkins_Test.java'
            }
        }
        stage('Test') {
            steps {
                //sh 'chmod 777 unitTests.xml'
                junit 'build/reports/**/*.xml'
                //sh 'cd src'
                //sh 'ls'
                //sh 'java jenkins_test.Jenkins_Test'
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
