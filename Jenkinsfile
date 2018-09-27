pipeline {
  agent any
  stages {
    stage('Checkout') {
      parallel {
        stage('Checkout') {
          steps {
            git(url: 'git@github.com:SalesRabbit/SalesRabbit-Android.git', branch: 'master', credentialsId: 'salesrabbit_jenkins')
          }
        }
        stage('error') {
          steps {
            sh 'cd Universal-Sales && git submodule update --init --recursive'
          }
        }
      }
    }
    stage('Test') {
      steps {
        dir(path: 'Universal-Sales') {
          sh './gradlew test'
        }

      }
    }
    stage('Build Debug') {
      steps {
        dir(path: 'Universal-Sales') {
          sh './gradlew assembleDebug'
        }

      }
    }
    stage('Archive APK') {
      steps {
        archiveArtifacts '**/*.apk'
      }
    }
  }
  environment {
    ANDROID_HOME = '/var/lib/jenkins/android-sdk-linux'
  }
}