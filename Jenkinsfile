properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('UnitTest') {
		git 'https://github.com/jamesdan0503/java-project.git'
		sh 'pwd'
		sh 'ls -l'
		sh 'ant -f ./test.xml -v'
		junit 'reports/result.xml'
	}   
	stage('Build') {    
		sh 'ant'
		sh 'ant -f build.xml -v'
	}
	stage('Deploy') {
		sh 'aws s3 cp /workspace/java-pipeline/dist/ s3://bucket/bucketforas10seis665 --recursive --exclude "*" --include "*.jar"'
	}

	stage('Report') {    
		junit 'reports/*.xml'
	}
}
