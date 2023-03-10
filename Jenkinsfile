
pipeline{
    agent any
    stages{
        stage('validating git'){
            steps{
                git branch: 'main', url: 'https://github.com/sumanthguthi705/aws.git'
            }
        }
        stage('unit testing'){
            steps{
                script{
                def mavenHome = tool name: "Maven-3.8.6", type:"maven"
                def mavenCMD = "${mavenHome}/bin/mvn"
                sh "${mavenCMD} test"
                }
            }
        }
        stage('Integration testing'){
            steps{
                script{
                def mavenHome = tool name: "Maven-3.8.6", type:"maven"
                def mavenCMD = "${mavenHome}/bin/mvn"
                sh "${mavenCMD} verify -DskipUnitTests"
                }
            }
        }
        stage('Maven Build'){
            steps{
                script{
                    def mavenHome = tool name: "Maven-3.8.6", type:"maven"
                    def mavenCMD = "${mavenHome}/bin/mvn"
                    sh "${mavenCMD} clean install"
                }
            }
        }
        stage('static code analysis'){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                        def mavenHome = tool name: "Maven-3.8.6", type:"maven"
                        def mavenCMD = "${mavenHome}/bin/mvn"
                        sh "${mavenCMD} clean package sonar:sonar"
                    }
                }
            }
        }
        stage('Quality gate analysis'){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
                }
            }
        }
        stage('Upload war files to nexus'){
            steps{
                script{
                    nexusArtifactUploader artifacts: 
                    [
                        [
                            artifactId: 'springboot',
                            classifier: '', file: 'target/Uber.jar',
                            type: 'jar'
                        ]
                    ],
                         credentialsId: 'NEXUSAUTH',
                         groupId: 'com.example', 
                         nexusUrl: '18.183.161.0:8081',
                         nexusVersion: 'nexus3', 
                         protocol: 'http',
                         repository: 'Success-Release',
                         version: '9.0.8'
                }
            }
        }
        stage('Deploy'){
            steps{
                script{
                    sshagent(['tomcat']) {
                        sh 'scp -o StrictHostKeyChecking=no target/Uber.jar tomcat@172.31.8.78:/opt/tomcat/webapps'
                    }
                }
            }
        }
    }
}
