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
        echo "code analysis"
      }
      stage('code quality'){
        "code quality"
      }
      stage('build'){
        echo "build"
      }
      stage('notification'){
        echo "notification"
      }
  }
}
