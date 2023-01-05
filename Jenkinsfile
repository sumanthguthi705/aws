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
                sh 'mvn test'
            }
        }
    }
}