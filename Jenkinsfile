 
pipeline{
    agent any
    tools{
        maven 'maven3'
    }
    stages{
        stage('Initialize'){
            steps{
                sh '''
                  echo "PATH=${PATH}"
                  echo "M2_HOME=${M2_HOME}"
                  '''
            }
        }
     stage('checkout stage'){
        steps{
            git 'https://github.com/divyasone/java-hello-world-webapp.git/'
        }
    }
    stage('Build-stage'){
        steps{
            sh 'mvn clean package'
            sh 'mv target/*.war target/demo.war'
        }
    }
    stage("deploy war file"){
        steps{
            sshagent(['ec2-id']) {
             sh "scp -o StrictHostKeyChecking=no target/demo.war ubuntu@172.31.10.125:/var/lib/tomcat9/webapps"
            }
        }
    }
}
}
