pipeline {

    environment {
        GROOVY_HOME = tool name: 'groovy 2.4.6', type: 'hudson.plugins.groovy.GroovyInstallation'
    }

    agent {
        node {
            label 'master'
            customWorkspace "C:/Users/francesca.seychell/Devops/customWorkspace"
        }
    }

    stages {
        stage(' Retrieve Source') { // Get code
            steps {
                 // get code from Git repository
                git branch: 'master', credentialsId: 'cb21cb62-bd2b-4f2a-855c-d7255ea9644a', url: 'https://github.com/fransey/springboot_app.git'
            }
        }

      
        stage('Build using Maven') { // Compile
            tools {
                maven 'mvnscm - 3.6.3'
            }
            steps {
                {
                    pom = readMavenPom file: "pom.xml";
                    pomVersion = "${pom.version}";
                }
                bat "mvn -DskipTests=true package"
            }
        }

        stage('Deploy to Nexus') {
            steps {
                bat "mvn -DskipTests=true -Dmaven.skipTests=true -f pom.xml clean package -Dversion=pomVersion deploy:deploy -DaltDeploymentRepository=localnexus::default::http://localhost:8081/repository/snapshots/"
            }
        }

    }
}
