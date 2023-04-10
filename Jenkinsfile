pipeline {
  agent {label 'agentfarm'}

  environment {
       SONAR_TOKEN = '89f2f7b0a761f8b048a7101cbc55f102e18abc75'
       SONAR_PROJECT_KEY = 'testing11_jenkins-sonar_testing' 
	 }
 
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }

 
  
  post {
    always {
      // Make sure to clean up any SonarCloud analysis data after the build
      cleanWs()
    }
  }
}

