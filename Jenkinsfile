properties([pipelineTriggers([githubPush()])])

node(‘linux’) {   
	stage('Test') {    
		git 'https://github.com/adrianelarson/java-project.git'
		sh 'ant -f test.xml -v'  
    junit 'reports/result.xml'
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}   
	stage('Results') {    
		  
	}
}