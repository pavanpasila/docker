Pipeline {
 agent any
  
  stages {
    stage ('stage SCM') {
      steps {
       git branch: 'main', credentialsId: 'pavan_github', url: 'https://github.com/pavanpasila/docker.git'
      } 
    }
   stage('stage maven') {
    steps {
     sh 'mvn clean install'
    }
   }
  }
}
