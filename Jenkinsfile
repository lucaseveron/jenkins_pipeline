pipeline {
    agent any
    environment {     
        DOCKERHUB_CREDENTIALS= credentials('dockerhubcredentials')     
    } 
    stages {
        stage('Eliminado de archivos viejo') {
            steps {
                dir ('TP6_App_docker') {
                    deleteDir()
                }
            }
        }
   
 
        stage('Eliminado de contendores viejo') {
            steps {
                sh 'docker container prune -f'
            }
        }
   
 
        stage('Descarga de la aplicacion desde Github') {
            steps {
                sh 'git clone https://github.com/gastonbarbaccia/TP6_App_docker.git'
                
            }
        }
   
   
        stage('Creando la imagen') {
            steps {
                sh 'cd TP6_App_docker && docker build -t lucaseveron/appjava:v1.0 .'
            }
        }
        
         stage('Ejecutando el contenedor') {
            steps {
                sh 'docker run -p 80:80 -p 7080:7080 -d --name app_front lucaseveron/appjava:v1.0'
            }
        }
        
        stage('Validando la web') {
            steps {
                sh "curl -LI http://localhost -o /dev/null -w '%{http_code}\n' -s"
            }
        }
        
        stage('Docker login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'                 
	            echo 'Login Completed' 
            }
        }
        
        stage('Docker push') {
            steps {
                sh 'docker push lucaseveron/appjava:v1.0'                 
                echo 'Push Image Completed'    
            }
        }

    }
    
}
