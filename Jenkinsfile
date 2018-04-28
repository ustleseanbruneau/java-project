properties([pipelineTriggers([githubPush()])])
node('linux') {
  git url: 'https://github.com/ustleseanbruneau/java-project.git', branch: 'master'
  stage('Unit Tests') {
    sh "ant -buildfile test.xml"
  }
  stage ("Build") {
    sh "ant -f build.xml -v"
  }
  stage ("Deploy") {
    sh "aws s3 cp /workspace/java-pipeline/dist/rectangle-${BUILD_NUMBER}.jar s3://ustleseanbruneau-seis665-asgn10"
  }
  stage ("Report") {
    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID',
	credentialsId: 'c7d991c0-5e8c-4f8d-90bb-77201202cdd6', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
	]]) {
	  sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins"
	}
  }
}
