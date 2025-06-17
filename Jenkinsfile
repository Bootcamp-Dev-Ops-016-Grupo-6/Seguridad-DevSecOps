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

        stage('Analisis de dependencias') {
            steps {
                bat 'mkdir dependency-check-report || echo "Directorio ya existe"'
                tool 'OWASP_DC_CLI'
                dependencyCheck odcInstallation: 'OWASP_DC_CLI', adittionalArguments: '--project "safenotes" --scan "target" --format "HTML" --format "XML" --out "dependency-check-report" --enableExperimental'
            }
        }

        stage('Test') {
            steps {
                bat 'npm test'
            }
        }
    }
}