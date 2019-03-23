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
                
                sh '${M2_HOME}/bin/mvn --batch-mode -V -U -e checkstyle:checkstyle spotbugs:spotbugs'
                recordIssues sourceCodeEncoding: 'UTF-8', 
                tool: groovyScript(parserId: 'groovy-id-in-system-config', pattern:'**/*report.log', reportEncoding:'UTF-8')
            }
        }
  }
  post {
       always {
            emailext attachLog: true, attachmentsPattern: 'README.md', body: 'Your job ${BUILD_URL} changed state', compressLog: true, subject: 'Jenkins Tests', to: 'a.sanchezdev@alumnos.urjc.es'
            junit testResults: '**/target/surefire-reports/TEST-*.xml'

            recordIssues enabledForFailure: true, tools: [mavenConsole(), java(), javaDoc()]
            recordIssues enabledForFailure: true, tool: checkStyle()
            
            
            
            
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
