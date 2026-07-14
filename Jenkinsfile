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
