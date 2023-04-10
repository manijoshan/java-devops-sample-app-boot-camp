pipeline {
  agent {label 'agentfarm'}

  environment {
       SONAR_TOKEN = '8e1bab6b2d917962c6585027caeb9bfec64df21e'
       SONAR_PROJECT_KEY = 'sonarqubereport' 
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

