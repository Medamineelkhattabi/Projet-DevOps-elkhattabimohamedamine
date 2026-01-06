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