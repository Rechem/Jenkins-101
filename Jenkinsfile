pipeline {
  agent any
  stages {
      stage ('Test'){
        steps {
            bat 'gradle test'
            archiveArtifacts 'build/test-results/test/*.xml'
            cucumber reportTitle: 'My report',
                     fileIncludePattern: '**/*.json'
        }
      }
      stage('Code Analysis'){
          steps{
              withSonarQubeEnv(installationName : 'SonarQube') {
                  bat 'gradle sonarqube'
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
      stage('Build'){
          steps{
              bat 'gradle build'
              bat 'gradle javadoc'
              archiveArtifacts 'build/docs/**/*.*'
              archiveArtifacts 'build/libs/**/*.*'
          }
      }
      stage('Deploy'){
          steps{
              bat "gradle publish"
          }
      }
      stage('Notification'){
          steps{
              notifyEvents message: 'This is a Jenkins automated message to let you know that a new version has been published !', title: 'New version released !', token: 'p-_GFdK1uAFCdwULUeSEHpn8iv4O9HSw'
          }
      }
  }
}
