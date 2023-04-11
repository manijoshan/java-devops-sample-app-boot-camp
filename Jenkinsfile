pipeline {
    agent any

    stages {
        stage('Install SonarScanner CLI') {
            steps {
                sh 'wget -O sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.6.2.2472-linux.zip'
                sh 'unzip -o -q sonar-scanner.zip'
                sh 'sudo rm -r /opt/sonar-scanner'
                sh 'sudo mv --force sonar-scanner-4.6.2.2472-linux /opt/sonar-scanner'
                sh 'sudo sh -c \'echo "#/bin/bash \nexport PATH=\\\"$PATH:/opt/sonar-scanner/bin\\\"" > /etc/profile.d/sonar-scanner.sh\''
                sh 'ls /opt/sonar-scanner/bin'
                sh 'chmod +x /opt/sonar-scanner/bin/sonar-scanner'
                sh 'echo $PATH'
                sh 'cat /etc/profile.d/sonar-scanner.sh'
                sh '. /etc/profile.d/sonar-scanner.sh'
                sh '/opt/sonar-scanner/bin/sonar-scanner --version'
                sh '/opt/sonar-scanner/bin/sonar-scanner -Dsonar.projectKey=manijoshan_java-devops-sample-app-boot-camp -Dsonar.organization=sonarqubereport -Dsonar.sources=. -Dsonar.host.url=https://sonarcloud.io  -Dsonar.login=8e1bab6b2d917962c6585027caeb9bfec64df21e'
            }
        }
    }
}
