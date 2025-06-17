pipeline {
    agent any

    tools {
        nodejs "safenotes"
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
                tool 'OWASP_DC_CLI'
                dependencyCheck odcInstallation: 'OWASP_DC_CLI', additionalArguments: '--project "safenotes" --scan . --format "HTML" --out "dependency-check-report" --enableExperimental'
            }
        }
    }
}