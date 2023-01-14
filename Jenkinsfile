pipeline {
  agent any
  stages {
      stage ('test'){
        steps {
            bat 'gradle test'
            archiveArtifacts 'build/reports'
            cucumber reportTitle: 'My report',
                     fileIncludePattern: '**/*.json'
        }
      }
      stage('code analysis'){
          steps{
              echo "code analysis"
          }
      }
      stage('code quality'){
          steps{
              echo "code quality"
          }
      }
      stage('build'){
          steps{
              echo "build"
          }
      }
      stage('notification'){
          steps{
              echo "notification"
          }
      }
  }
}
