pipeline {
        agent any
        tools {
            maven 'MAVEN3'
        }
        stages {
            stage('Build') {
                steps {
                    git url: 'https://github.com/InigoAgirre/Testing.git', branch: 'main'
                    sh 'mvn clean compile'
                }
            }
            stage("SonarQube analysis") {
                steps {
                    withSonarQubeEnv('sonarqube') {
                        sh 'mvn verify sonar:sonar -Dsonar.host.url=http://denetmu.duckdns.org:9000/'
                    }
                }
            }
            stage("Quality Gate") {
                steps {
                    timeout(time: 1, unit: 'HOURS') {
                        waitForQualityGate abortPipeline: true
                    }
                }
            }
        }
}
