pipeline {
    agent any
    stages {
        stage('Construir') {
            steps {
                sh 'docker build -t DevMasters:latest .'
            }
        }
        // RAMA DE PRUEBAS
        stage('Despliegue a Test') {
            when { branch 'develop' } // 
            steps {
                script {
                    sh 'kubectl apply -f k8s/deployment.yaml -n pruebas'
                    sh 'kubectl rollout restart deployment/DevMasters -n pruebas'
                }
            }
        }
        // RAMA DE PRODUCCIÓN
        stage('Despliegue a Prod') {
            when { branch 'main' } // 
            steps {
                script {
                    sh 'kubectl apply -f k8s/deployment.yaml -n produccion'
                    sh 'kubectl rollout restart deployment/DevMasters -n produccion'
                }
            }
        }
    }
}