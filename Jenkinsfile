pipeline {
  agent none
  stages {
    stage('Build & Test') {
      agent {
        node {
          label 'docker'
        }

      }
      steps {
        sh 'mvn -Dmaven.test.failure.ignore clean package'
        stash(name: 'build-test-artifacts', includes: '**/target/surefire-reports/Test-*.xml,target/*.jar')
      }
    }

    stage('Report  & Publish') {
      agent {
        node {
          label 'docker'
        }

      }
      steps {
        unstash 'build-test-artifacts'
        junit '**/target/surefire-reports/Test-*.xml'
        archiveArtifacts(artifacts: 'target/*.jar', onlyIfSuccessful: true)
      }
    }

  }
}