pipeline {
  agent any

  environment {
    SONAR_TOKEN = credentials('sonar-token')
    SONAR_PROJECT_KEY = 'my-project'
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
          sh 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=testing11_jenkins-sonar_testing'
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

