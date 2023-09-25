pipeline {
  agent any
  tools {
    maven 'Maven_3_9_4'
  }

  stages {
    stage('CompileandRunSonarAnalysis') {
      steps {
        withCredentials([string(credentialsId: 'Sonar-Token', variable: 'Sonar-Token')]) {
          sh("mvn -Dmaven.test.failure.ignore verify sonar:sonar -Dsonar.login=${Sonar-Token} -Dsonar.projectKey=devsecops-ci -Dsonar.host.url=http://localhost:9000/")
        }
      }
    }
    stage('Build') {
      steps {
        withDockerRegistry([credentialsId: "dockerhub-credentials", url: ""]) {
          script {
            app = docker.build("shameem2001/devsecops-build")
          }
        }
      }
    }
    stage('RunContainerScan') {
      steps {
        withCredentials([string(credentialsId: 'snyk-token', variable: 'snyk-token')]) {
          script {
            try {
              sh("snyk container test shameem2001/devsecops-build")
            } catch (err) {
              echo err.getMessage()
            }
          }
        }
      }
    }
    stage('RunSnykSCA') {
      steps {
        withCredentials([string(credentialsId: 'snyk-token', variable: 'snyk-token')]) {
          sh("mvn snyk:test -fn")
        }
      }
    }
    stage('RunDASTUsingZAP') {
      steps {
        sh("/home/shameem/ZAP_2.12.0_Crossplatform/ZAP_2.12.0/zap.sh -port 9393 -cmd -quickurl https://www.example.com -quickprogress -quickout C:\\zap\\ZAP_2.12.0_Crossplatform\\ZAP_2.12.0\\Output.html")
      }
    }

    stage('checkov') {
      steps {
        sh("checkov -s -f main.tf")
      }
    }

  }
}
