properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('UnitTest') {
		git 'https://github.com/jamesdan0503/java-project.git'
		sh 'ant'
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'
	}   
	stage('Build') {    
		sh 'ant'
		sh 'ant -f build.xml -v'
	}

	stage('Report') {
		sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
	}
}
