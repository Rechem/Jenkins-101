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
    bat echo "code analysis"
  }
  stage('code quality'){
    bat echo "code quality"
  }
  stage('build'){
    bat echo "build"
  }
  stage('notification'){
    bat echo "notification"
  }
}
