pipeline {
 agent any
  
  stages {
    stage ('stage SCM') {
      steps {
       git branch: 'master', url: 'https://github.com/pavanpasila/docker-hello-world-spring-boot.git'
      } 
    }
   stage('stage maven') {
    steps {
     sh 'mvn clean install'
    }
   }
   stage('buid docker') {
    steps {
     sh 'docker build -t hello-world .'
    }
   }
  }
}
