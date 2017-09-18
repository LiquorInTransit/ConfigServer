node {
   stage('ConfigPreparation') {
   		git 'https://github.com/LiquorInTransit/ConfigServer.git'
   }
   stage('ConfigBuild') {
        sh "mvn package"
   }
   stage('ConfigDeploy') {      
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'awscredentials', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
         ansiblePlaybook credentialsId: 'ssh-credentials', installation: 'ansible-installation', playbook: 'deploy.yaml', sudoUser: null
      }      
   }
   
//Now Build and Deploy the DiscoveryService

   stage('DiscoveryPreparation') {
   		git 'https://github.com/LiquorInTransit/DiscoveryService.git'
   }
   stage('DiscoveryBuild') {
        sh "mvn package"
   }
   stage('DiscoveryDeploy') {      
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'awscredentials', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
         ansiblePlaybook credentialsId: 'ssh-credentials', installation: 'ansible-installation', playbook: 'discoveryDeploy.yaml', sudoUser: null
      }      
   }
   
//   stage('TriggerDiscoveryBuild') {
//   		if (env.BRANCH_NAME == 'master') {
//		    build job: '../DiscoveryService/master', wait: false
//		}
//   }
}