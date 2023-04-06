pipeline{
    agent {label "agentfarm" }
    stages {
           stage('Installing Maven'){
               steps {
                   sh 'sudo apt-get update -y && sudo apt-get upgrade -y'
                   sh 'sudo apt-get install -y wget tree unzip maven'
           }
      }
stage('Compiling and Running Test Cases') {
       steps {
              sh 'mvn clean'
           	  sh 'mvn compile'
              sh 'mvn test'
       }
}
     stage('Creating Package') {
       steps {
           	   sh 'mvn package'
       }
}
     stage('Deploying Application') {
       steps {
          	   script{
                     withEnv(['JENKINS_NODE_COOKIE=dontkill']) {
                            sh 'nohup java -jar ./target/springboot-bootcamp-0.0.1-SNAPSHOT.jar &'
                     }
           	   }
       }
}
}
      stage('sonar-deploy') {
        steps {
version: 0.2
env:
    parameter-store:
      SONAR_TOKEN : 89f2f7b0a761f8b048a7101cbc55f102e18abc75
phases:
  install:
    runtime-versions:
      nodejs: 14
  pre_build:
    commands:
      - mkdir /downloads/sonarqube -p
      - cd /downloads/sonarqube
      - wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.2.0.1873-linux.zip
      - unzip sonar-scanner-cli-4.2.0.1873-linux.zip
      - mv sonar-scanner-4.2.0.1873-linux /opt/sonar-scanner
      - echo -e "sonar.host.url=http://sonarscan.dev.bhubportal.com \n  sonar.sourceEncoding=UTF-8 \n sonar.qualitygate.wait=true " >> /opt/sonar-scanner/conf/sonar-scanner.properties
      - echo -e "#/bin/bash \n export PATH='$PATH:/opt/sonar-scanner/bin'" >> /etc/profile.d/sonar-scanner.sh
      - . /etc/profile.d/sonar-scanner.sh
      - sonar-scanner -v
  build:
    commands:
      - export NPM_TOKEN=`aws secretsmanager get-secret-value --secret-id npm-token --query SecretString --output text`
      - cd ../..
      - cd /codebuild/output/src*/src
      - npm i
      - sonar-scanner -Dsonar.projectKey=BHub_be_graphqlAPI -Dsonar.sources=. -Dsonar.host.url=http://sonarscan.dev.bhubportal.com  -Dsonar.login=$SONAR_TOKEN

}
