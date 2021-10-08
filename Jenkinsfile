pipeline {
  agent any
  stages {
    stage('Build & Test') {
      steps {
        sh 'mvn --file  Ch03/example-maven-project/pom.xml -Dmaven.test.failure.ignore clean package'
        stash(name: 'build-test-artifacts', includes: '**/target/surefire-reports/Test-*.xml,target/*.jar')
      }
    }

    stage('Report  & Publish') {
      steps {
        unstash 'build-test-artifacts'
        junit '**/target/surefire-reports/Test-*.xml'
        archiveArtifacts(artifacts: 'target/*.jar', onlyIfSuccessful: true)
      }
    }

  }
}