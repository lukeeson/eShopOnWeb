pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'dotnet build eShopOnWeb.sln'
      }
    }

    stage('TEST UNIT') {
      parallel {
        stage('TEST UNIT') {
          steps {
            sh 'dotnet test tests/UnitTests'
          }
        }

        stage('Integration') {
          steps {
            sh 'dotnet test tests/IntegrationTests'
          }
        }

        stage('Functional') {
          steps {
            sh 'tests/FunctionalTests'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        sh '  dotnet publish eShopOnWeb.sln -o /var/aspnet  -p:ErrorOnDuplicatePublishOutputFiles=false'
      }
    }

  }
}