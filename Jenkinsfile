pipeline {
    agent any
    options { skipDefaultCheckout() }
    stages {
		stage('Checkout') {
            steps {
                // Get some code from a GitHub repository
                git url:'https://github.com/thapabhesh/eShopOnWeb.git', branch:'main'               
                
            }
           
        }
        stage('Build') {
            steps {                
                bat 'dotnet build eShopOnWeb.sln'
            }
           
        }
        
        stage('Test') {
            steps {
                bat 'dotnet test ./tests/UnitTests/UnitTests.csproj --logger:\"trx;logFileName=%WORKSPACE%\\tests\\unittest.xml\"'
            }
            
            post {
                always {
                    //xUnitDotNet(MSTest(pattern: 'tests\\*.xml'))
                    xunit([MSTest(pattern: 'tests\\*.xml')])
                }
            }
        }
    }
}
