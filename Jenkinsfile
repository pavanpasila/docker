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
   stage('buid docker image') {
    steps {
     sh 'docker build -t hello-world .'
     sh 'docker images' 
    }
   }
   stage ('push images to jfrog') {
    steps {
      sh 'docker login  $JFROG_URL -u $JFROG_USER -p $JFROG_PWD'
      sh 'docker tag hello-world $JFROG_URL/docker-repo/$BUILD_NUMBER'
    }
   }
  }
}
