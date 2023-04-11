pipeline{
   agent any
	environment {
       SONAR_TOKEN = '8e1bab6b2d917962c6585027caeb9bfec64df21e'
       SONAR_PROJECT_KEY = 'manijoshan_java-devops-sample-app-boot-camp'
         }

   stages{
   stage('Installing Maven'){
      steps {
          sh 'sudo apt-get update -y && sudo apt-get upgrade -y'
          sh 'sudo apt-get install -y wget tree unzip maven'
           }
        }
     
  
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage('SonarQube analysis') {
      steps {
        withSonarQubeEnv('sonarqubeserver') {
         
	 sh 'mvn sonar:sonar \ -Dsonar.projectKey=$SONAR_PROJECT_KEY \ -Dsonar.login=$SONAR_TOKEN'
        }
      }
    }
}}
