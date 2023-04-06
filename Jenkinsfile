pipeline {
  agent any

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

    stage('SonarQube Scan') {
      steps {
        withSonarQubeEnv('SonarCloud') {
          sh 'mvn sonar:sonar -Dsonar.projectKey=$SONAR_PROJECT_KEY -Dsonar.login=$SONAR_TOKEN'
	 }
      }
    }
    
    stage('Quality Gate') {
      steps {
        timeout(time: 1, unit: 'HOURS') {
          waitForQualityGate abortPipeline: true
        }
      }
    }
  }
  
  post {
    always {
      // Make sure to clean up any SonarCloud analysis data after the build
      cleanWs()
    }
  }
}

