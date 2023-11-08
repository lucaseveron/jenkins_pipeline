pipeline {
    agent any
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
                sh 'git clone https://github.com/gastonbarbaccia/TP6_App_docker'
                
            }
        }
   
   
        stage('Creando la imagen') {
            steps {
                sh 'cd TP6_App_docker && docker build -t lucas/appjava:v1.0 .'
            }
        }
        
         stage('Ejecutando el contenedor') {
            steps {
                sh 'docker run -p 80:80 -p 7080:7080 -d --name app_front lucas/appjava:v1.0'
            }
        }
        
        stage('Validando la web') {
            steps {
                sh "curl -LI http://localhost -o /dev/null -w '%{http_code}\n' -s"
            }
        }
        
    }
}