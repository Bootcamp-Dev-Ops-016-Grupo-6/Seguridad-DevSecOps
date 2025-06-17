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
                dependencyCheck odcInstallation: 'OWASP_DC_CLI', additionalArguments: '--project "safenotes" --scan "." --format "HTML" --format "XML" --out "dependency-check-report" --enableExperimental'
            }
        }
    }
}