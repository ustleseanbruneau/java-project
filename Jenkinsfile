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
    sh "aws s3 cp ./rectangle-${BUILD_NUMBER} s3://ustleseanbruneau-seis665-asgn10"
  }
  stage ("Report") {
    sh "env"
  }
}
