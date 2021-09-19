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
     sh 'docker build -t hello-world:$BUILD_NUMBER .'
     sh 'docker images' 
    }
   }
   stage ('push images to jfrog') {
    steps {
      sh 'docker login  $JFROG_URL -u $JFROG_USER -p $JFROG_PWD'
      sh 'docker tag hello-world:$BUILD_NUMBER $JFROG_URI/docker-repo/hello-world/$BUILD_NUMBER'
      sh 'docker push $JFROG_URI/docker-repo/hello-world/$BUILD_NUMBER'
    }
   }
   stage ('pull from jfrog and deploy to application server') {
    steps {
     script {
      def remote = [:]
       remote.name = $APP_NAME
       remote.host = $APP_IP
       remote.user = $APP_USER
       remote.password = $APP_PWD
       remote.allowAnyHosts = true
      sshCommand remote: remote, command: "docker login  $JFROG_URL -u $JFROG_USER -p $JFROG_PWD" 
      sshCommand remote: remote, command: "docker pull $JFROG_URI/docker-repo/hello-world/$BUILD_NUMBER"
      sshCommand remote: remote, command: "docker run -itd -p 8080:8080 $JFROG_URI/docker-repo/hello-world/$BUILD_NUMBER"
     }
    }
   }
   }
}
