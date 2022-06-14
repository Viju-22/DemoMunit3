pipeline
{
    agent any
    
    stages{
        
        stage('SonarQube analysis') {
            steps {
            withSonarQubeEnv('SonarQube') {
            bat 'mvn sonar:sonar -Dsonar.sources=src/ -Dsonar.host.url=http://localhost:9000 -Dsonar.login=c91a76d35e003f1d1af99856195a65522c327514'
            }
            }
            }
       
        
        stage("Quality gate") {
            steps {
            waitForQualityGate abortPipeline: true
            }
            }
    
        stage('Build Application'){
            steps{
        bat 'mvn clean package -DskipTests'
        }	
        }
        
        stage('Munit Testing'){
         steps{
        bat 'mvn clean test'
        }     
        }
             
        stage('Deploy Application To Mulesoft'){
         steps{
        bat 'mvn package deploy -DmuleDeploy -DconnectedAppClientId=1b508c93ec364822a86822319b28d1a2 -DconnectedAppClientSecret=C35aCD1ACa1b4c33812810c15E7BbCC0'
        }
       
        }
       
   
    }
}
