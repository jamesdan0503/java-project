properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('UnitTest') {    
		sh 'ant'
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'
	}   
	stage('Build') {    
		sh 'ant'
		sh 'ant -f build.xml -v'
	}   
	stage('Deploy') {
	
	}
	
	stage('Report') {    
		junit 'reports/*.xml'   
	}
}
