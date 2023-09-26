pipeline {
  agent any
  tools {
    maven 'MAVEN'
  }

  stages {
    // stage('CompileandRunSonarAnalysis') {
    //   steps {
    //     withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
    //       sh('mvn -Dmaven.test.failure.ignore verify sonar:sonar -Dsonar.login=$SONAR_TOKEN -Dsonar.projectKey=devsecops-ci -Dsonar.host.url=http://localhost:9000/')
    //     }
    //   }
    // }
    // stage('Build') {
    //   steps {
    //     withDockerRegistry([credentialsId: "dockerhub-credentials", url: ""]) {
    //       script {
    //         app = docker.build("shameem2001/devsecops-build")
    //       }
    //     }
    //   }
    // }
    // stage('RunContainerScan') {
    //   steps {
    //     withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
    //       script {
    //         try {
    //           sh('snyk auth $SNYK_TOKEN')
    //           sh("snyk container test shameem2001/devsecops-build")
    //         } catch (err) {
    //           echo err.getMessage()
    //         }
    //       }
    //     }
    //   }
    // }
    // stage('RunSnykSCA') {
    //   steps {
    //     withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
    //       sh("mvn snyk:test -fn")
    //     }
    //   }
    // }
    // stage('RunDASTUsingZAP') {
    //   steps {
    //     sh("/home/shameem/ZAP_2.12.0_Crossplatform/ZAP_2.12.0/zap.sh -port 9393 -cmd -quickurl https://www.example.com -quickprogress -quickout /home/shameem/ZAP_2.12.0_Crossplatform/ZAP_2.12.0/Output.html")
    //   }
    // }

    stage('checkov') {
      steps {
        sh("/home/shameem/checkov -s -f main.tf")
      }
    }

  }
}
