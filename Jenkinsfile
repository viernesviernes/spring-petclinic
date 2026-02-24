pipeline {
    agent any

    triggers {
        // Currently set to every 1 minute on Tuesday (Day 2) for your screenshots
        cron('H/1 * * * 2')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Test with Coverage') {
            steps {
                // FIX: Use mvnw.cmd for Windows and remove the './'
                bat 'mvnw.cmd clean verify' 
            }
        }
    }

    post {
        always {
            // Simplified JaCoCo call to avoid plugin version errors
            jacoco()
            
            // Archives the .jar file
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}
