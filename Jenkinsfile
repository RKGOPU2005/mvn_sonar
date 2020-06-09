pipeline {
        agent any
        stages {
            /* "Build" and "Test" stages omitted */
            stage('GIT Checkout') {
                steps {
                  git url : 'https://github.com/RKGOPU2005/mvn_sonar.git'
                }
            }
            stage('Build') {
				steps {
					withSonarQubeEnv('sonar') {
						sh '/opt/maven/bin/mvn clean verify sonar:sonar -Dmaven.test.skip=true'
					}
				}
			}          
            stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
    }
}
