pipeline {
    agent any

    environment {
        PROJECT_DIR = "/opt/wordpress_project"
        BACKUP_SCRIPT = "/opt/wordpress_project/data/backup/wordpress_s3_backup.sh"
        GIT_REPO = "https://github.com/ProRaj144/wordpress-deployment.git"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "Stage 1: Pulling latest code from GitHub..."
                git branch: 'main', url: "${GIT_REPO}"
                echo "Code pulled successfully."
            }
        }

        stage('Deploy Docker Stack') {
            steps {
                echo "Stage 2: Deploying WordPress stack..."
                sh '''
                cd $PROJECT_DIR
                docker compose down || true
                docker compose up -d --build
                '''
                echo "Docker stack deployed successfully."
            }
        }

        stage('Backup to S3') {
            steps {
                echo "Stage 3: Running backup to S3..."
                sh "bash ${BACKUP_SCRIPT}"
                echo "Backup completed and uploaded to S3."
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline executed successfully — deployment and backup done."
        }
        failure {
            echo "❌ Pipeline failed — please check Jenkins logs for details."
        }
    }
}
