import hudson.model.*;
import java.util.regex.Matcher;
import jenkins.util.*;
import jenkins.model.*;
import jenkins.scm.*;
import groovy.json.*;

pipeline {

    environment {
       GROOVY_HOME = tool name: 'groovy 2.4.6', type: 'hudson.plugins.groovy.GroovyInstallation'
        // This can be nexus3 or nexus2
        NEXUS_VERSION = "nexus3"
        // This can be http or https
        NEXUS_PROTOCOL = "http"
        // Where your Nexus is running
        NEXUS_URL = "localhost:8081"
        // Repository where we will upload the artifact
        NEXUS_REPOSITORY = "snapshots"
        // Jenkins credential id to authenticate to Nexus OSS
        NEXUS_CREDENTIAL_ID = "1f55913a-7c89-4360-8e13-773db17ebba8"
   
    }
	
  agent {
        node {
            label 'master'
            customWorkspace "C:/Users/francesca.seychell/Devops/demo-workspace"
        }
    }
  stages {
    stage(' Retrieve Source') { // Get code
      steps {
        // get code from Git repository
        git branch: 'master', credentialsId: 'cb21cb62-bd2b-4f2a-855c-d7255ea9644a', url: 'https://github.com/seycf13/Demo-Devops.git'
      }
    }
	stage('Retreive POM Data') {
          steps {
            script {
                pom = readMavenPom file: "${pom_location}"
                groupid = "${pom.groupId}";
                artifactid = "${pom.artifactId}";
                pomVersion = "${pom.version}";
		println("GroupID: " + groupid)
                println("ArtifactID: " + artifactid)
                println("Version: " + version)
            }
          }
	  
  }
}
}
