pipeline {
  agent any

  environment {
    MAVEN_ARGS=" -B -e -U"
  }

  stages {

        stage('Build') {
            steps {
                withMaven(maven: 'MAVEN_ENV') {
                    sh "mvn clean install -DskipTests=true -Dmaven.javadoc.skip=true -Dcheckstyle.skip=true ${MAVEN_ARGS}"
                }
            }
        }

        stage('OWASP Dependency-Check') {
            steps {
                dependencyCheck additionalArguments: '''
                            -o './'
                            -s './'
                            -f 'ALL'
                            --prettyPrint''', odcInstallation: 'OWASP-DP-CHECK'

                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }
 }
}  
