  def Workspace = "/var/jenkins_home"
  def Creds = "aws-id"
  def region = "ap-south-1"
  def image = "kl-uaa-service"
  def registryUrl = "146776836293.dkr.ecr.ap-south-1.amazonaws.com/${image}"	
	pipeline {
		agent any
		environment {
		git_commit_hash = sh(script: 'git describe --tags --always', returnStdout: true).trim()
		}
   		stages {
			stage('Git Checkout') {
				steps {
					git branch: 'master',
	//					credentialsId: 'Gitlab-pvtkey',
							url: 'https://github.com/hemanthg7824/gradle-sample-app.git'
					}
			}	
			stage('Docker Build and Push'){
				steps{
	
        			script {	
						withDockerRegistry([credentialsId: "jfrog credential", url: 'http://18.215.151.55:8081/artifactory']) {
			
				echo "build"
				sh "docker build -t testweb ."

				echo "push"
				sh "docker push testweb"
						  }
						}
					  }

					}
			stage('Deploy-Upgrade on K8s'){
				steps{
					echo "Deploy"
					sh "ansible-playbook ${Workspace}/${image}/ansible/deploy.yaml --extra-vars registryUrl=${registryUrl} --extra-vars git_commit_hash=${git_commit_hash}"
					}
				}

}
}
