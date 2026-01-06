pipeline {
    agent any
    
    tools {
        maven 'Maven-3.9'
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo '=== Récupération du code depuis GitHub ==='
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo '=== Build du projet avec Maven ==='
                sh 'mvn clean install -DskipTests'  // sh pour Linux/Docker
            }
        }
        
        stage('Test') {
            steps {
                echo '=== Exécution des tests ==='
                sh 'mvn test'  // sh pour Linux/Docker
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('Archive') {
            steps {
                echo '=== Archivage des artefacts ==='
                archiveArtifacts artifacts: '**/target/*.jar', 
                                 fingerprint: true,
                                 allowEmptyArchive: true
            }
        }
        
        stage('Deploy') {
            steps {
                echo '=== Déploiement de l\'application ==='
                echo 'Application déployée avec succès sur le serveur local!'
            }
        }
        
        stage('Notify Slack') {
    steps {
        echo '=== Notification Slack ==='
        script {
            slackSend(
                channel: '#devops-notifications',
                color: 'good', // vert pour succès
                message: """
                ✅ Build #${env.BUILD_NUMBER} terminé avec succès!
                Projet: ${env.JOB_NAME}
                Durée: ${currentBuild.durationString}
                Lien: ${env.BUILD_URL}
                """.stripIndent(),
                tokenCredentialId: 'slack-token', // l'ID du token que tu as ajouté dans Jenkins
                botUser: true // très important pour utiliser ton token bot
            )
        }
    }
}

    }
    
    post {
    success {
        echo '✅ Pipeline exécuté avec succès!'
        slackSend(
            channel: '#devops-notifications',
            color: 'good',
            message: "✅ *Pipeline Réussi!* ${env.JOB_NAME} #${env.BUILD_NUMBER} - Durée: ${currentBuild.durationString}",
            tokenCredentialId: 'slack-token',
            botUser: true
        )
    }
    failure {
        echo '❌ Le pipeline a échoué.'
        slackSend(
            channel: '#devops-notifications',
            color: 'danger',
            message: "❌ *Pipeline Échoué!* ${env.JOB_NAME} #${env.BUILD_NUMBER} - Vérifier les logs: ${env.BUILD_URL}console",
            tokenCredentialId: 'slack-token',
            botUser: true
        )
    }
    always {
        echo '=== Nettoyage ==='
    }
}

}