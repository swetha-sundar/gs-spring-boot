node {
   stage('init') {
      checkout scm
   }
   stage('build') {
      def mvnHome = tool name: 'Apache Maven 3.6.3', type: 'maven'
      echo "MAVEN HOME"
      echo mvnHome
      pwd
      ls
      sh "${mvnHome}/bin/mvn clean package"
      sh '''
         cd target
         cp ../complete/src/main/resources/web.config web.config
         cp todo-app-java-on-azure-1.0-SNAPSHOT.jar app.jar 
         zip todo.zip app.jar web.config
      '''
   }
   stage('deploy') {
      azureWebAppPublish azureCredentialsId: env.AZURE_CRED_ID,
      resourceGroup: env.RES_GROUP, appName: env.WEB_APP, filePath: "**/todo.zip"
   }
}
