pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/udayjy/newjava.git'
                }
            }
        }
        stage('UNIT testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                }
            }
        }
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                }
            }
        }
        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'git') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                   }
                    
                }
            }
            stage('nexus repo store'){
                
                steps{
                    
                    script{
                        
                          nexusArtifactUploader artifacts: 
                              [
                                [
                                  artifactId: 'springboot', 
                                    classifier: '', file: 'target/Uber.jar', type: 'jar'
                                ]
                              ], 
                              credentialsId: 'nexus', 
                              groupId: 'com.example', 
                              nexusUrl: '15.168.60.148:8081', 
                              nexusVersion: 'nexus2', 
                              protocol: 'http', 
                              repository: 'release', 
                              version: '1.0.0'
                    }
                }
            }
        }
        
}
