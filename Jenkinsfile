pipeline {
    agent any
    parameters {
        choice(name: 'ENTORNO', choices: ['staging', 'produccion'], description: 'Entorno de despliegue')
        booleanParam(name: 'EJECUTAR_DEPLOY', defaultValue: false, description: '¿Desplegar al finalizar?')
    }
    environment {
        APP_NAME = "jenkins-demo-app"
    }
    options {
        timestamps()
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }
    stages {
        stage('Checkout') {
            steps {
                echo "Clonando repositorio..."
                checkout scm
            }
        }
        stage('Instalar dependencias') {
            steps {
                sh 'node -v'
                echo "No hay dependencias externas en este demo"
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
                archiveArtifacts artifacts: 'dist/**', fingerprint: true
            }
        }
        stage('Deploy') {
            when {
                expression { return params.EJECUTAR_DEPLOY }
            }
            steps {
                echo "Desplegando ${env.APP_NAME} en el entorno: ${params.ENTORNO}"
                // Aquí iría tu script real de despliegue
            }
        }
    }
    post {
        success {
            echo " ✅  Pipeline completado correctamente para ${env.APP_NAME}"
            
            // Nuevo correo de éxito
            mail to: 'ferkev230@gmail.com',
                 subject: "✅ Build Exitoso: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "¡Todo salió perfecto! El código pasó las pruebas y se construyó correctamente. Detalles: ${env.BUILD_URL}"
        }
        failure {
            echo " ❌  El pipeline falló. Revisa los logs de la etapa correspondiente."
            
            // El correo de fallo que ya habías corregido
            mail to: 'ferkev230@gmail.com',
                 subject: "❌ Build fallido: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Revisa la consola: ${env.BUILD_URL}"
        }
        always {
            echo "Build #${env.BUILD_NUMBER} finalizado."
        }
    }
}
}