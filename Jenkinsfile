pipeline {
    agent any

    tools {
        maven "Maven"
    }

    stages {
        stage('Build') {
            steps {
                
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/AK9773/spring-boot-demo1.git'

              

               
                 bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

          
        }

        stage('StartTomcat') {
            steps {
               bat '''c:
                    cd D:\\apache-tomcat-8.0.53\\apache-tomcat-8.0.53\\bin
                    set JAVA_HOME=C:\\Program Files\\Java\\jdk1.8.0_221
                    startup.bat'''
            }

          
        

         stage('Deploy') {
            steps {
               deploy adapters: [tomcat8(credentialsId: 'tomcat-credential', path: '', url: 'http://localhost:9999/')], contextPath: null, onFailure: false, war: '**/*.war'
            }

          
        }
    }
}