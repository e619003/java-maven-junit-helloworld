pipeline {
  agent any
  stages {
    stage('checkout project') {
      steps {
        checkout scm
      }
    }

    stage('Run') {
      steps {
        sh 'mvn -Dmaven.test.failure.ignore=true clean package'
      }
    }

    stage('Report') {
      parallel {
        stage('Report') {
          steps {
            junit '**/target/surefire-reports/TEST-*.xml'
          }
        }

        stage('Archive') {
          steps {
            archiveArtifacts 'target/*.jar'
          }
        }

      }
    }

  }
}