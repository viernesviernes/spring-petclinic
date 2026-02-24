pipeline {
    agent any

    triggers {
        // Trigger every 5 minutes only on Mondays (Day 1)
        cron('H/5 * * * 1')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Test with Coverage') {
            steps {
                // Runs Maven test and generates JaCoCo report
                bat './mvnw clean verify' 
            }
        }
    }

    post {
        always {
            // This plugin must be installed in Jenkins to work
            jacoco buildContext: [[]], 
                   execPattern: '**/target/*.exec', 
                   classPattern: '**/target/classes', 
                   sourcePattern: '**/src/main/java'
            
            // Archives the .jar file as an artifact
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}
