pipeline {
    agent any
    
    tools {
        maven 'Maven-3.9'  // ⚠️ Remplacez par le nom exact de votre Maven
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
                bat 'mvn clean install -DskipTests'  // bat pour Windows
            }
        }
        
        stage('Test') {
            steps {
                echo '=== Exécution des tests ==='
                bat 'mvn test'
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
                // Vous pouvez ajouter des commandes de déploiement ici
            }
        }
        
        stage('Notify Slack') {
            steps {
                echo '=== Notification Slack ==='
                script {
                    def message = """
                    ✅ Build #${env.BUILD_NUMBER} terminé avec succès!
                    Projet: ${env.JOB_NAME}
                    Durée: ${currentBuild.durationString}
                    """.stripIndent()
                    echo message
                    
                    // La vraie notification Slack sera configurée après
                }
            }
        }
    }
    
    post {
        success {
            echo '✅ Pipeline exécuté avec succès!'
        }
        failure {
            echo '❌ Le pipeline a échoué.'
        }
        always {
            echo '=== Nettoyage ==='
        }
    }
}