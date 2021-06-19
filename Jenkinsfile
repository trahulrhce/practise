#!/usr/bin/env groovy
build_dependents_repo = git@url

pipeline {
  agent {
    label 'Jenkins slave'
  }
  environment {
    EMAIL_TO = 'DL or specific email ids'
  }

  stages {
    stage('cleanworkspace') {
      steps {
        cleanWs()
      }
    }

    stage('git checkout'){
    steps {
      checkout([$class: 'GitSCM', branches: [
            [name: * /<branch-name>]], [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'directory name wher you want your code to checkout' [
              [credentialsId: 'github login token', url: build_dependents_repo]]])
        }
  }
      stage('dependency installs') {
        steps {
                sh 'pip install -r requirements.txt'
        }   
    }
      stage('python build'){
      steps {
        sh 'python test.py'
      }
    }
  }
 post {
    failure {
        emailtext body: 'build status body'
        to: DL or emailids
        subject: 'Build success/failed/unstable/etc $PROJECT_NAME - $BUILD_NUMBER'
      }
    }
  }
