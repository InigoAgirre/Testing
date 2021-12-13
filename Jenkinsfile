pipeline {
        agent any
        tools {
            maven 'Maven'
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
                        sh 'mvn verify sonar:sonar -Dsonar.host.url=http://denetmu.duckdns.org:9000/ -Dsonar.projectKey=prueba -Dsonar.projectName=Prueba'
                    }
                }
            }
             stage("Quality Gate") {
                steps {
                    timeout(time: 5, unit: 'MINUTES') {
                        waitForQualityGate abortPipeline: true
                    }
                }
      }     
    }
}
