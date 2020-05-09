import hudson.model.*;
import java.util.regex.Matcher;
import jenkins.util.*;
import jenkins.model.*;
import jenkins.scm.*;
import groovy.json.*;

pipeline {

    environment {
       GROOVY_HOME = tool name: 'groovy 2.4.6', type: 'hudson.plugins.groovy.GroovyInstallation'

   
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
	cleanWs()
        // get code from Git repository
        git branch: 'master', credentialsId: 'cb21cb62-bd2b-4f2a-855c-d7255ea9644a', url: 'https://github.com/seycf13/Demo-Devops.git'
      }
    }
	
	stage('Retreive POM Data') {
          steps {
		  script {
		pom = readMavenPom file: "pom.xml";
		groupid = "${pom.groupId}";
                artifactid = "${pom.artifactId}";
                pomVersion = "${pom.version}";
            }
          }
		  }
		  
		
	stage('Build using Maven') { // Compile
     tools {
        maven 'mvnscm - 3.6.3'
    }
    steps {
             bat "mvn -DskipTests=true package"
         }
      }
	  
	 stage('Deploy to Nexus') {
         steps {
             bat "mvn -DskipTests=true -Dmaven.skipTests=true -f pom.xml clean package -Dversion=${pom.version} deploy:deploy -DaltDeploymentRepository=localnexus::default::http://localhost:8081/repository/snapshots/"
         }
      }	
	  
  }
}
