pipeline {
    agent any
    environment {
        // Définition des variables d'environnement
        DOCKER_IMAGE = 'devops:latest'
        CONTAINER_NAME = 'devops'
    }
    triggers {
        // Ce pipeline pourrait être déclenché par un webhook en pratique, ici nous le déclenchons manuellement ou par un sondage SCM
    }
    stages {
        stage('Checkout') {
            steps {
                // Extraction du code source
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                // Construction de l'image Docker
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }
        stage('Stop and Remove existing Docker container') {
            steps {
                // Arrêt et suppression du conteneur Docker existant, si nécessaire
                script {
                    def runningContainer = sh(script: "docker ps -q -f name=${CONTAINER_NAME}", returnStdout: true).trim()
                    if (runningContainer) {
                        sh "docker stop ${CONTAINER_NAME}"
                        sh "docker rm ${CONTAINER_NAME}"
                    }
                }
            }
        }
        stage('Run Docker container') {
            steps {
                // Démarrage d'un nouveau conteneur Docker
                script {
                    sh "docker run -d --name ${CONTAINER_NAME} -p 8080:80 ${DOCKER_IMAGE}"
                }
            }
        }
        stage('Deploy') {
            steps {
                // Simulation d'un déploiement, similaire à l'action GitHub pour déployer sur GitHub Pages
                echo "Déploiement simulé. Dans un cas réel, cette étape pourrait déployer le contenu sur un serveur web ou une plateforme de cloud."
            }
        }
    }
    post {
        always {
            echo 'Nettoyage post-exécution...'
            // Ici, vous pouvez ajouter des commandes pour le nettoyage après l'exécution du pipeline, si nécessaire
        
        }
    }
}
