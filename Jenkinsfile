<<<<<<< HEAD
def COLOR_MAP = [

    'SUCCESS': 'good', 

    'FAILURE': 'danger',

    'UNSTABLE': 'danger'

]
=======
>>>>>>> 987224863605c79095065ea7918f143fff82717a
pipeline {
  agent {
    label 'Maven-Build-Env' // Use the Maven slave node for this pipeline
  }
  stages {
    stage('Validate Project') {
        steps {
            sh 'mvn validate'
        }
    }
    stage('Unit Test'){
        steps {
            sh 'mvn test'
        }
    }
    stage('Integration Test'){
        steps {
            sh 'mvn verify -DskipUnitTests'
        }
    }
    stage('App Packaging'){
        steps {
            sh 'mvn package'
        }
    }
    stage ('Checkstyle Code Analysis'){
        steps {
            sh 'mvn checkstyle:checkstyle'
        }
    }
    stage('SonarQube Inspection') {
        steps {
            sh  """mvn sonar:sonar \
                   -Dsonar.projectKey=maven-java-webapp \
                   -Dsonar.host.url=http://172.31.31.199:9000 \
                   -Dsonar.login=15e92bac1f1b554181c4d1fbab4bb5be6278fd92"""
        }
    }
    stage("Upload Artifact To Nexus"){
        steps{
             sh 'mvn deploy'
        }
        post {
            success {
              echo 'Successfully Uploaded Artifact to Nexus Artifactory'
        }
      }
    }
  }
  post {

    always {

        echo 'Slack Notifications.'

        slackSend channel: '#benny-jenkins-master-clients-alerts', //update and provide your channel name

        color: COLOR_MAP[currentBuild.currentResult],

        message: "*${currentBuild.currentResult}:* Job Name '${env.JOB_NAME}' build ${env.BUILD_NUMBER} \n Build Timestamp: ${env.BUILD_TIMESTAMP} \n Project Workspace: ${env.WORKSPACE} \n More info at: ${env.BUILD_URL}"

    }

  }
}
