pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Cypress - Chrome') {
            steps {
                sh 'npx cypress run --browser chrome --spec "cypress/e2e/imdb_nicolas_cage.cy.js"'
            }
            post {
                always {
                    junit 'cypress/results/*.xml'
                    archiveArtifacts artifacts: 'cypress/screenshots/**, cypress/videos/**', allowEmptyArchive: true
                }
            }
        }

        stage('Cypress - Firefox') {
            steps {
                sh 'npx cypress run --browser firefox --spec "cypress/e2e/imdb_nicolas_cage.cy.js"'
            }
            post {
                always {
                    junit 'cypress/results/*.xml'
                    archiveArtifacts artifacts: 'cypress/screenshots/**, cypress/videos/**', allowEmptyArchive: true
                }
            }
        }   
    post {
        success {
            echo "✅ Todas las pruebas IMDb pasaron correctamente."
        }
        failure {
            echo "❌ El pipeline falló. Revisar reportes y artefactos."
        }
    }
}
