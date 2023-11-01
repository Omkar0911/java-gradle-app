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
                    timeout(time: 15, unit: 'MINUTES') {
                        def qp = waitForQualityGate()
                        if (qb.status !='OK') {
                            error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }
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