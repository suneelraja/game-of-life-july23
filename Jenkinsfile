pipeline {
    agent { label 'JDK_8' }
    options {
        retry(3)
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        jdk 'JAVA_8'
    }
    stages {
        stage('code') {
            steps {
                git url: 'https://github.com/dummyrepos/game-of-life-july23.git',
                    branch: 'master'
            }
        }
        stage('package') {
            steps {
                sh script: 'mvn clean package'
            }

        }
        stage('report') {
            steps {
                junit testResults: '**/surefire-reports/TEST-*.xml'
                archiveArtifacts artifacts: '**/target/gameoflife.war'
            }

        }
    }
    post {
        success {
            mail subject: 'your project is effective',
                 body: 'your project is effective',
                 to: 'all@qt.com'
        }
        failure {
            mail subject: 'your project is defective',
                 body: 'your project is defective',
                 to: 'all@qt.com'
        }
    }
}