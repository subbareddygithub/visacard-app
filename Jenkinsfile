node('maven-label') {
   def mvnHome
   stage('Preparation') { 
      
      git credentialsId: 'ubuntu', url: 'https://github.com/subbareddygithub/visacard-app.git'
                 
      mvnHome = tool 'maven'
   }
   stage('Build') {
      
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean deploy sonar:sonar -Dsonar.host.url="http://172.31.33.58:9000/"'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
}
