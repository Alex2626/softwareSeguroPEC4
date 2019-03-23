pipeline {
  agent any
  tools {
        maven 'M3'
        jdk 'JDK8'
    }
  stages {
    stage('Prepara') {
        steps {
            git "https://github.com/Alex2626/softwareSeguroPEC4"
            
        }
    }
    stage('Test1') {
        steps {
            sh '${M2_HOME}/bin/mvn --batch-mode -V -U -e checkstyle:checkstyle '
            
        }
    }
    stage ('Analysis') {
            steps {
                sh '${M2_HOME}/bin/mvn --batch-mode -V -U -e checkstyle:checkstyle '
            }
        }
  }
  post {
       always {
            junit testResults: '**/target/surefire-reports/TEST-*.xml'

            recordIssues enabledForFailure: true, tools: [mavenConsole(), java(), javaDoc()]
            recordIssues enabledForFailure: true, tool: checkStyle()
            
            emailext body: '''Hello Alejandro,
            Your job ${BUILD_URL} changed state to ${currentBuild.result}.
            Cheers,
            Jenkins''', attachmentsPattern:'README.md' , attachLog: true, compressLog: true, subject: 'Reporte Job ${JOB_NAME} changed status', to: 'a.sanchezdev@alumnos.urjc.es'
            
       }
       success{
            sh 'cp -r DVWA-master /var/www/html/dvwa'
           // sh 'mv -f /var/www/html/dvwa/config/config* /var/www/html/dvwa/config/config.inc.php'
            sh 'chmod -R 755 DVWA-master && service mysql start && service apache2 start'
           
       }
        
        failure {
            sh 'echo FLUJO CANCELADO'
           
    
        }
    }
    
}
