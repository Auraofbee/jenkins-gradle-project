def COLOR_MAP = [

    'SUCCESS': 'good', 

    'FAILURE': 'danger',

    'UNSTABLE': 'danger'

]
pipeline {
  agent {
    label 'Gradle-Build-Env' // Use the Gradle slave node for this pipeline
  }
  stages {
    stage('Validate Project') {
        steps {
            sh 'gradle check'
        }
    }
    stage('Gradle Project Tasks'){
        steps {
            sh 'gradle tasks'
        }
    }
    stage('Unit & Integration Test'){
        steps {
            sh 'gradle test'
        }
    }
    stage('Package Application'){
        steps {
            sh 'gradle build'
        }
    }
    stage ('Checkstyle Code Analysis'){
        steps {
            sh 'gradle checkstyleTest'
        }
    }
    stage('SonarQube Inspection') {
        steps {
            sh 'gradle sonarqube'
            sh  """mvn sonar:sonar \
                   -Dsonar.projectKey=maven-java-webapp \
                   -Dsonar.host.url=http://172.31.31.199:9000 \
                   -Dsonar.login=15e92bac1f1b554181c4d1fbab4bb5be6278fd92"""
        }
        }
    }
    stage("Upload Artifact To Nexus"){
        steps {
            sh 'gradle publish'
        }
        post {
            success {
                echo 'Successfully Uploaded Artifact to Nexus Artifactory'
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
  }

