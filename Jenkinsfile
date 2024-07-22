pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Vict0rK/Vulnerable-Web-Application.git'
            }
        }
        
        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube'
                    
                    // Print the path of SonarQube scanner
                    sh "echo SonarQube Scanner Path: ${scannerHome}"
                    
                    // Run SonarQube scanner
                    withSonarQubeEnv('SonarQube') {
                        sh """
                            ${scannerHome}/bin/sonar-scanner \
                            -Dsonar.projectKey=OWASP \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://192.168.10.142:9000 \
                            -Dsonar.token=sqp_pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Vict0rK/Vulnerable-Web-Application.git'
            }
        }
        
        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube'
                    
                    // Print the path of SonarQube scanner
                    sh "echo SonarQube Scanner Path: ${scannerHome}"
                    
                    // Run SonarQube scanner
                    withSonarQubeEnv('SonarQube') {
                        sh """
                            ${scannerHome}/bin/sonar-scanner \
                            -Dsonar.projectKey=OWASP \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://192.168.10.142:9000 \
                            -Dsonar.token=sqp_73b59d5f97e5c6d2fbe0a1a08b128b39ba84395d
                        """
                    }
                }
            }
        }
    }
    
    post {
        always {
            recordIssues enabledForFailure: true, tools: [sonarQube()]
        }
    }
}
                        """
                    }
                }
            }
        }
    }
    
    post {
        always {
            recordIssues enabledForFailure: true, tools: [sonarQube()]
        }
    }
}
