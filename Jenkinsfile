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
            def mavenHome = tool name: "Maven-3.8.6", type:"maven"
            def mavenCMD = "${mavenHome}/bin/mvn"
            steps{
                sh "${mavenCMD} mvn test"
            }
        }
    }
}
