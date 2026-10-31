```groovy
pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo 'Cloning ShopKart repository...'
                git branch: 'main',
                    url: 'https://github.com/Jyoti-V11-Bhosale/ShopKart-CI-CD.git'
            }
        }

        stage('Build and Deploy') {
            steps {
                sh '''
                    echo "Building Docker image..."
                    docker build -t shopkart:latest .

                    echo "Stopping old container if it exists..."
                    docker stop shopkart || true

                    echo "Removing old container if it exists..."
                    docker rm shopkart || true

                    echo "Starting new ShopKart container..."
                    docker run -d \
                        --name shopkart \
                        --restart unless-stopped \
                        -p 80:80 \
                        shopkart:latest

                    echo "ShopKart deployment completed!"
                '''
            }
        }
    }

    post {
        success {
            echo 'ShopKart was built and deployed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the Jenkins console output.'
        }
    }
}
```