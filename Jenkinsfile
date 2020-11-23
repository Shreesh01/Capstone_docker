library identifier: 'jenkins-shared@master', retriever: modernSCM(
 [$class: 'GitSCMSource',
  remote: 'https://github.com/Shreesh01/Capstone_docker.git',
 ])

pipeline {
 environment {
  appName = "server"
  registry = "shreesh01/capstone"
  registryCredential = "shreesh01"
  projectPath = "/jenkins/data/workspace/project"
 }

 agent any

 stages {

  stage('Build Image') {
   steps {
    script {
      dockerImage = docker.build "$registry:latest"
     } 
    }
   }

  stage('Deploy Image') {
   steps {
    script {
      docker.withRegistry("$registryURL", registryCredential) {
      dockerImage.push()
      }
    }
   }
  }
 }
}

def getBuildName() {
 "${BUILD_NUMBER}_$appName:${params.RELEASE_TAG}"
}

def isMaster() {
 "${params.RELEASE_TAG}" == "master"
}
