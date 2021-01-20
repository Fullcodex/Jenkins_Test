pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                //sh 'help'
                //sh 'makefile' 
                //archiveArtifacts artifacts: '**/src/*.jar', fingerprint: true
                sh 'javac src/jenkins_test/Jenkins_Test.java'
            }
        }
        stage('Test') {
            steps {
                /* `make check` returns non-zero on test failures,
                * using `true` to allow the Pipeline to continue nonetheless
                */
                //sh 'make check || true' 
                sh 'chmod 777 unitTests.xml'
                junit 'unitTests.xml'
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
