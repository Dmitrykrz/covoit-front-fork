pipeline {
    agent any
    stages {

      stage('==================================Backup==================================') {
            steps {                
                sh 'sudo cp -r /var/www/html /var/www/html.backup'
                
            }
        }

      
        stage("==================================Dependances==================================") {
            steps {
               
                sh 'sudo apt-get update'
                sh 'sudo apt-get install -y apache2'
                sh 'sudo systemctl start apache2'
            }
        }
        stage('Checkout') {
            steps {
                
                echo '=========================Checkout========================='
                git branch: 'main', url: 'https://github.com/Dmitrykrz/covoit-front-fork'
                sh 'ls'
            }
        }
        stage('Deploy') {
            steps {
                 echo '=========================Deploy=================================='
                 sh 'npm install'
                 sh ' npm run build'
                sh 'cp -r dist/gestion-des-transports-front/browser/* /var/www/html'
                
            }
        }
        stage('==================================Test==================================') {
            steps {
               sh 'curl http://localhost'
               sh 'curl http://localhost | grep -q "GestionDesTransportsFront" || (echo "ERROR: GestionDesTransportsFront not found!" && exit 1)'
            }
        }
    }
    post {
        success {
            echo 'All is good !'
            sh 'sudo rm -rf /var/www/html.backup'          
        }
        failure {
           
            echo 'Pipeline failed!'         
          sh 'sudo cp -r /var/www/html.backup/* /var/www/html/'
          
        }
        
    
   always {
            echo '=========================Cleanup========================='
                   
                
                
               sh 'sudo rm -rf /var/www/html/*'
               sh 'sudo rm -rf /var/www/html.backup'
               
        }}
}
