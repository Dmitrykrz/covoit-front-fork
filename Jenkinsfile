pipeline {
    agent any
    stages {
        stage("Dependances") {
            steps {
               
                sh 'sudo apt-get update'
                sh 'sudo apt-get install -y apache2'
                sh 'sudo systemctl start apache2'
            }
        }
        stage('Checkout') {
            steps {
                
                echo 'checkout'
                git branch: 'main', url: 'https://github.com/Dmitrykrz/covoit-front-fork'
                sh 'ls'
            }
        }
        stage('Deploy') {
            steps {
                 echo 'deploy'
                 sh 'npm install'
                 sh ' npm run build'
                sh 'cp dist/gestion-des-transports-front/browser/* /var/www/html'
                
            }
        }
        stage('Test') {
            steps {
                echo 'curl localhost'
            }
        }
    }
    post {
        success {
            echo 'All is good !'
            // Action en cas de succès
        }
        failure {
           
            echo 'Pipeline failed!'
        }
        always {
           echo 'always'
        }
    }
}
