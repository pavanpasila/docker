Pipeline {
 agent any
  
  stages {
    stage ('stage SCM') {
      steps {
       git branch: 'main', url: 'https://github.com/pavanpasila/docker.git'
      } 
    }
   stage('stage maven') {
    steps {
     sh 'mvn clean install'
    }
   }
  }
}
