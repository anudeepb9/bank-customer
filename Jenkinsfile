pipeline {
  agent any
  tools { 
        maven 'Maven'
        jdk 'JAVA'
  }
  stages {
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace... */
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
        sh 'echo $USER'
        sh 'echo whoami'
      }
    }
    stage('Docker Build') {
      steps {
        sh '/usr/bin/docker build -t pavan9999/dev:bank-customer .'
      }
    }
    stage('Push image') {
      steps {
        withDockerRegistry([credentialsId: 'Docker-Hub', url: "https://index.docker.io/v1/"]) {
          sh '/usr/bin/docker push pavan9999/dev:bank-customer'
        }
      }
    }
  }
}
