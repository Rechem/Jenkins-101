pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                bat 'gradle test';
                junit 'build/test-results/test/*.xml'
                cucumber 'target/report.json'
            }
        }
        stage('Code Analysis') {
            steps {
                withSonarQubeEnv(installationName: 'SonarQube') {
                    bat 'gradle sonarqube';
                }
            }
        }
        stage('Code Quality') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage('Build') {
            steps {
                bat 'gradle build';
                bat 'gradle javadoc';
                archiveArtifacts 'build/docs/**/*.*';
                archiveArtifacts 'build/libs/**/*.*';
            }
        }
        stage('Deploy') {
            steps {
                bat "gradle publish";
            }
        }
    }
    post {
        success {
            mail to: 'ir_chadouli@esi.dz',
                    body: "This is a Jenkins automated message to let you know that a new version has been published !",
                    charset: 'UTF-8',
                    subject: "New version released !";
            notifyEvents message: 'This is a Jenkins automated message to let you know that a new version has been published !',
                    title: 'New version released !', token: 'p-_GFdK1uAFCdwULUeSEHpn8iv4O9HSw';
        }
        failure {
            mail to: 'ir_chadouli@esi.dz',
                    body: "This is a Jenkins automated message to let you know that the most recent build has failed.",
                    charset: 'UTF-8',
                    subject: "Build failed.";
        }
    }
}