pipeline {
    agent any
    stages{
	stage ('checkout') {
	    steps{
		    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/raamstar/simple-reactjs-app.git']]])
	}
	}
	    
	stage('Submit Stack') {
            steps {
		    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws-key', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {	     
				    powershell "aws cloudformation create-stack --stack-name myteststack --template-body file://stack.json --region us-east-1"
		    }
          }    
  }
}
}
