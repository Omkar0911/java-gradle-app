pipeline{
      agent any
      stages{
         stage("Sonar Quality Check") {
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                        sh 'chmod +x gradlew'
                        sh './gradlew sonarqube --info'
                    }
                }
            }
         }
      }
      post{
          success{
              echo "========pipeline executed successfully ========"
          }
          failure{
              echo "========pipeline execution failed========"
          }
      }
  }