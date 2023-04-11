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
	  sh 'sudo apt install openjdk-11-jdk -y'
         sh 'sudo apt-get install -y wget tree unzip maven'
	sh 'wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.2.0.1873-linux.zip'
	sh 'unzip sonar-scanner-cli-4.2.0.1873-linux.zip -y'
	sh 'sudo mv sonar-scanner-4.2.0.1873-linux /opt/sonar-scanner'
	sh 'echo -e "sonar.host.url=http://sonarscan.dev.bhubportal.com \n  sonar.sourceEncoding=UTF-8 \n sonar.qualitygate.wait=true " >> /opt/sonar-scanner/conf/sonar-scanner.properties'
           }
}}
}
