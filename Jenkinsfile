pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Vict0rK/Vulnerable-Web-Application.git'
            }
        }

        stage('Install Node.js') {
            steps {
                script {
                    // Check if Node.js is installed
                    def nodeVersion = sh(script: 'node -v || echo "not found"', returnStdout: true).trim()

                    if (nodeVersion == "not found") {
                        echo "Node.js not found. Installing..."
                        sh '''
                        # Download Node.js binaries
                        curl -fsSL https://nodejs.org/dist/v16.17.0/node-v16.17.0-linux-x64.tar.xz -o node.tar.xz
                        # Extract the binaries
                        mkdir -p $HOME/node
                        tar -xf node.tar.xz -C $HOME/node --strip-components=1
                        # Add Node.js to PATH
                        export PATH=$HOME/node/bin:$PATH
                        # Verify installation
                        node -v
                        '''
                    } else {
                        echo "Node.js version: ${nodeVersion}"
                    }
                }
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
