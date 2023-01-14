pipeline {
  agent any
  stages {
      stage ('test'){
        steps {
            bat 'gradle test'
            archiveArtifacts 'build/reports/*'
            cucumber reportTitle: 'My report',
                     fileIncludePattern: '**/*.json'
        }
      }
      stage('code analysis'){
          steps{
              bat echo "code analysis"
          }
      }
      stage('code quality'){
          steps{
              bat echo "code quality"
          }
      }
      stage('build'){
          steps{
              bat echo "build"
          }
      }
      stage('notification'){
          steps{
              bat echo "notification"
          }
      }
  }
}
