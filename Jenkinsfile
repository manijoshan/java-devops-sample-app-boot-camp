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
    environment {
    SONAR_TOKEN = '89f2f7b0a761f8b048a7101cbc55f102e18abc75'
    SONAR_PROJECT_KEY = 'testing11_jenkins-sonar_testing'
  }
  
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

