<<<<<<< HEAD
=======
<<<<<<< HEAD
>>>>>>> 38fe32f1bf1ce5f1432382d5673ad641e0cc81ea
def COLOR_MAP = [

    'SUCCESS': 'good', 

    'FAILURE': 'danger',

    'UNSTABLE': 'danger'

]
<<<<<<< HEAD

pipeline {
  agent {
    label 'Gradle-Build-Env' // Use the Gradle slave node for this pipeline
=======
=======
>>>>>>> 987224863605c79095065ea7918f143fff82717a
pipeline {
  agent {
    label 'Maven-Build-Env' // Use the Maven slave node for this pipeline
>>>>>>> 38fe32f1bf1ce5f1432382d5673ad641e0cc81ea
  }
  stages {
    stage('Validate Project') {
        steps {
<<<<<<< HEAD
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
=======
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
>>>>>>> 38fe32f1bf1ce5f1432382d5673ad641e0cc81ea
        }
    }
    stage ('Checkstyle Code Analysis'){
        steps {
<<<<<<< HEAD
            sh 'gradle checkstyleTest'
=======
            sh 'mvn checkstyle:checkstyle'
>>>>>>> 38fe32f1bf1ce5f1432382d5673ad641e0cc81ea
        }
    }
    stage('SonarQube Inspection') {
        steps {
<<<<<<< HEAD
            sh 'gradle sonarqube'
=======
            sh  """mvn sonar:sonar \
                   -Dsonar.projectKey=maven-java-webapp \
                   -Dsonar.host.url=http://172.31.31.199:9000 \
                   -Dsonar.login=15e92bac1f1b554181c4d1fbab4bb5be6278fd92"""
>>>>>>> 38fe32f1bf1ce5f1432382d5673ad641e0cc81ea
        }
    }
    stage("Upload Artifact To Nexus"){
        steps{
<<<<<<< HEAD
            sh 'gradle publish'
        }
        post {
            success {
                echo 'Successfully Uploaded Artifact to Nexus Artifactory'
=======
             sh 'mvn deploy'
        }
        post {
            success {
              echo 'Successfully Uploaded Artifact to Nexus Artifactory'
>>>>>>> 38fe32f1bf1ce5f1432382d5673ad641e0cc81ea
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
<<<<<<< HEAD

=======
>>>>>>> 38fe32f1bf1ce5f1432382d5673ad641e0cc81ea
