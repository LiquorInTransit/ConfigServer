node {
   stage('Preparation') {
   		git 'https://github.com/LiquorInTransit/ConfigServer.git'
   }
   stage('Build') {
        sh "mvn package"
   }
   stage('Deploy') {      
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'awscredentials', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
         ansiblePlaybook credentialsId: 'ssh-credentials', installation: 'ansible-installation', playbook: 'deploy.yaml', sudoUser: null
      }      
   }
//  stage('TriggerDiscoveryBuild') {
//  		if (env.BRANCH_NAME == 'master') {
//		    build job: '../DiscoveryService/master', wait: false
//		}
//   }
}