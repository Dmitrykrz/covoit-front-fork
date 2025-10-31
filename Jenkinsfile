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
            }
        }
        stage('Deploy') {
            steps {
                 echo 'deploy'
                
            }
        }
        stage('Test') {
            steps {
               
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
