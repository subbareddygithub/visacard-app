node('maven-label') {
   def mvnHome
   stage('Preparation') { 
      
      git credentialsId: 'ubuntu', url: 'https://github.com/subbareddygithub/visacard-app.git'
                 
      mvnHome = tool 'maven'
   }
   stage('Build') {
      
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
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
