pipeline {
  agent any
  stages {
      stage ('test'){
        steps {
            bat 'gradle test'
            archiveArtifacts 'build/test-results/test/*.xml'
            cucumber buildStatus: 'FAILURE',
                     reportTitle: 'My report',
                     fileIncludePattern: '**/*.json'
        }
      }
      stage('code analysis'){
          steps{
              withSonarQubeEnv(installationName : 'SonarQube') {
                  bat 'gradle sonarqube'
              }
          }
      }
      stage('code quality') {
          steps {
              timeout(time: 1, unit: 'HOURS') {
                  waitForQualityGate abortPipeline: true
              }
          }
      }
      stage('build'){
          steps{
              bat 'gradle build'
              bat 'gradle javadoc'
              archiveArtifacts 'build/docs/**/*.*'
              archiveArtifacts 'build/libs/**/*.*'
          }
      }
      stage('deploy'){
          steps{
              bat "gradle publish"
          }
      }
      stage('notification'){
          steps{
              echo "notification"
          }
      }
  }
}
