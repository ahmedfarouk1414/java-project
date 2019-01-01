pipeline {
  agent  none 


  stages {

    stage('Unit Tests') {
    agent {
       lable 'apache'
      }
      steps {
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
      }
   }
 
     stage('build') {
         agent {
        lable 'apache'
        }

      steps {
        sh 'ant -f build.xml -v'
        }
   
       post {
    success {
       archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
   }
  }
}


    stage('deploy') {
          agent {
            lable 'apache'
            }

     steps {
      sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/"
          }
         }
  
    stage ("Runing on CentOS") {
     agent {
        lable 'CentOS'
      }
     steps {
        sh "wget http://192.168.122.225/recmtangles/all/${env.BUILD_NUMBER}.jar"
        sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 4"
      }
     }
   }
  } 
