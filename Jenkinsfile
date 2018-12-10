pipeline {
   agent any 
  stages {
     stage('Checkout') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '9e612bee-967f-4172-a07a-a36df0a85b62', url: 'https://github.com/GANKNIR/content-jenkins-pipeline_working.git']]])
      }
    }
    stage('build') {
      steps {
        sh 'javac -d . src/*.java'
        sh 'echo Main-Class: Rectangulator > MANIFEST.MF'
        sh 'jar -cvmf MANIFEST.MF rectangle.jar *.class'
      }
    }
    stage('run') {
      steps {
        sh 'java -jar rectangle.jar 7 9'
       // sh 'mkdir -p /var/www/html/rectangles/{all,green}'
       // sh 'chown jenkins:jenkins -R /var/www/html/rectangles'
       // sh 'cp /var/jenkins_home/workspace/pipeline/rectangle.jar /var/www/html/rectangles'
      }
     }
  }  
  /* stage('deploy') {
      steps {
        sh 'mkdir -p /var/www/html/rectangles/nikhil2'
        sh 'chown jenkins:jenkins -R /var/www/html/rectangles/nikhil2'
        sh 'cp /var/jenkins_home/workspace/pipeline/rectangle.jar /var/www/html/rectangles/nikhil2'
      }
     } */
  post {
    success {
      archiveArtifacts artifacts: 'rectangle.jar', fingerprint: true
    }
  }
 
}
