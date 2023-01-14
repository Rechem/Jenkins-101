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
              withSonarQubeEnv('SonarQube') {
              }
          }
      }
      steps {
          timeout(time: 1, unit: 'HOURS') {
              waitForQualityGate abortPipeline: true
          }
      }
      stage('build'){
          steps{
              bat 'gradle build'
              bat 'gradle javadoc'
              archiveArtifacts 'build/docs'
              archiveArtifacts 'build/libs'
          }
      }
      stage('notification'){
          steps{
              bat echo "notification"
          }
      }
  }
}
