properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Unit Test') {    
		git 'https://github.com/adrianelarson/java-project.git'
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}   
	stage('Deploy') {    
		sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle*.jar s3://jenkins-s3bucket-17s3y9bthgv0y/'   
	} 
	stage('Report') {    
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
}  
	}
}

