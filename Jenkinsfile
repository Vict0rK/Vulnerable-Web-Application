pipeline {
    agent {
        docker {
            image 'node:16'
            args '-u root' // This allows you to run commands as the root user to install packages
        }
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Vict0rK/Vulnerable-Web-Application.git'
            }
        }

        stage('Install Java') {
            steps {
                sh '''
                apt-get update
                apt-get install -y openjdk-11-jdk
                '''
                // Set JAVA_HOME environment variable
                sh 'echo "export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64" >> ~/.bashrc'
                sh 'echo "export PATH=$JAVA_HOME/bin:$PATH" >> ~/.bashrc'
                sh 'source ~/.bashrc'
            }
        }

        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    // Define the SonarQube scanner tool
                    def scannerHome = tool 'SonarQube'

                    // Print the path of SonarQube scanner
                    sh "echo SonarQube Scanner Path: ${scannerHome}"

                    // Run the SonarQube scanner
                    withSonarQubeEnv('SonarQube') {
                        sh """
                        ${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=OWASP \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://192.168.10.142:9000 \
                        -Dsonar.token=sqp_e0288076aa1977cdcfe6445723aeef2080c2b8c8
                        """
                    }
                }
            }
        }
    }

    post {
        always {
            recordIssues enabledForFailure: true, tool: sonarQube()
        }
    }
}
