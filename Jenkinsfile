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
	stage('Deploy') {
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '9c02272a-44c3-4440-a976-6be6ab49c54b', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    		// some block
		sh 'aws s3 cp /workspace/java-pipeline/dist/ s3://bucket/bucketforas10seis665 --recursive --exclude "*" --include "*.jar"'
		}

	}

	stage('Report') {    
		junit 'reports/*.xml'
	}
}
