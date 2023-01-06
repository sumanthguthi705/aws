//OM
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
        stage('Maven Build')
        {
            steps{
                script{
                    def mavenHome = tool name: "Maven-3.8.6", type:"maven"
                    def mavenCMD = "${mavenHome}/bin/mvn"
                    sh "${mavenCMD} clean install"
                }
            }
        }
    }
}
