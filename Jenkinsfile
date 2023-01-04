pipeline {
  agent { label 'gradle' }

  stages {
    
    stage('Build') {
      steps {
        withGradle {
           sh 'gradle clean build --stacktrace -i'
        }
      }
    } // Build

    stage('Post') {
      steps {
        script {
          jacoco()
          junit 'lib/build/test-results/test/*.xml'
          def pmd = scanForIssues tool: [$class: 'Pmd'], pattern: 'lib/build/reports/pmd/*.xml'
          publishIssues issues: [pmd]
        }
      }
    } // Post

  }
}