pipeline{
agent any
tools {
        maven "maven3"
    }

stages{
        stage("scm"){
            steps{
                git credentialsId: 'gethub_credentials', url: 'https://github.com/umasrireddy/spring3-mvc-maven-xml-hello-world.git'
                }
              }
      stage("build"){
            steps{
              sh 'mvn package'
                }
              } 
          stage('deploy') {
             steps{
                 withCredentials([usernameColonPassword(credentialsId: 'remote_tomcat_credentials', variable: 'tomcatcred')]) {
          sh "curl -v -u uma:uma $tomcatcred -T /var/lib/jenkins/workspace/git-maven/target/spring3-mvc-maven-xml-hello-world-1.0-SNAPSHOT.war 'http://ec2-15-206-203-74.ap-south-1.compute.amazonaws.com:8081/manager/text/deploy?path=/tomcat-pipeline&update=true'"
                }
             } 
       post {
               failure {
                     script {
                 currentBuild.result = 'FAILURE'
                                  }
                                   }
                     always {
                       step([$class: 'Mailer',
                         notifyEveryUnstableBuild: true,
                         recipients: "kasi.umamaheswari7@gmail.com",
                         sendToIndividuals: true])
                             }
                     }
                }
             
            }
       }

    
