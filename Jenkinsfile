pipeline {
    agent any

    tools {
        nodejs "safenotes"
        jdk "JDK-17"
    }

    environment {
        PATH = "${tool 'safenotes'}/node_modules/.bin:${env.PATH}"
    }

    stages {
        stage('Install') {
            steps {
                bat 'npm install'
            }
        }

        stage('Test') {
            steps {
                bat 'npm test'
            }
        }
        
        stage('Analisis de dependencias') {
            steps {
                bat 'if not exist dependency-check-report mkdir dependency-check-report'
                tool 'OWASP_DC_CLI'
                dependencyCheck odcInstallation: 'OWASP_DC_CLI', additionalArguments: '--project "safenotes" --scan . --format "HTML" --out "dependency-check-report" --enableExperimental'
            }
        }
    }
}