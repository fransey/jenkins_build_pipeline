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
        // get code from Git repository
        git 'https://github.com/seycf13/Demo-Devops.git'
      }
    }
    stage('Compile') { // Compile
     tools {
        maven 'mvnscm - 3.6.3'
    }
    steps {
             bat "mvn -DskipTests=true package"
         }
      }
	
 stage('Deploy to Nexus') {
         steps {
             bat "mvn -DskipTests=true -Dmaven.skipTests=true -f ${env.pom_location} clean package -Dversion=${version} deploy:deploy -DaltDeploymentRepository=nexus::default::${repository}"
         }
      }	
	  
  }
}
