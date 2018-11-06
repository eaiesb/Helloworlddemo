#!/usr/bin/groovy
pipeline {
    environment {
        JAVA_HOME = tool('java')
    }
agent any
options {
disableConcurrentBuilds()
}
stages {
  
stage("buildsrc") {
steps { buildsrc() }
}
stage('renaming the target zip file') {
    steps {
               sh 'mv target/helloworld-1.0.0-SNAPSHOT-mule-application.jar helloworld.jar'
    }
}  
stage("Buildimg") {
steps { 
	
	buildApp() }
}
stage("Deploy") {
  steps { deploy() 
	  
	}
}
stage("CloudDeploy") {
  steps { clouddeploy()
	}
}	
}
}
// steps
def buildsrc() {
dir ('.' ) {
    sh '/app/ciplatform/apache-maven-3.3.9/bin/mvn clean install'
}
}
def buildApp() {
dir ('' ) {
def appImage = docker.build("eaiesbhub/mule-4:${BUILD_NUMBER}")
}
}
def clouddeploy() {
    dir ('.' ) {
    sh '/app/ciplatform/apache-maven-3.3.9/bin/mvn clean package deploy'
    }
}	
