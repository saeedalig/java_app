@Library("my-shared-lib") _

pipeline {

    agent any

    parameters {
        choice (name: 'action', choices: 'Create\nDelete', description: 'Choose Create/Destroy')
        string (name: 'imageName', description: "name of the docker build", defaultValue: 'java_app')
        string (name: 'imageTag',  description: "tag of the docker build", defaultValue: 'v1')
        string (name: 'dockerHub', description: "name of the Docker user", defaultValue: 'asa96')
    }
    
    stages {

        stage ("Git Checkout") { 
            when {expression {params.action == 'Create'} }
            steps {
                script {
                    gitCheckout(
                        branch: "main",
                        url: "https://github.com/saeedalig/java_app.git"
                    )
                }
            }
        }

        stage ("MVN Unit Test") {
            when {expression {params.action == 'Create'} }
            steps {
                script {
                    mvnTest()
                }
            }
        }

        stage ("MVN Integration Test") {
            when {expression {params.action == 'Create'} }
            steps {
                script {
                    mvnIntegrationTest()
                }
            }
        }

        stage ("Static Code Analysis: SonarQube") {
            when {expression {params.action == 'Create'} }
            steps {
                script {
                    def SonarQubecredentialsId = 'sonar-api'
                    staticCodeAnalysis(SonarQubecredentialsId)
                }
            }
        }

        stage ("Quality Gate Status Check: SonarQube") {
            when {expression {params.action == 'Create'} }
            steps {
                script {
                    def SonarQubecredentialsId = 'sonar-api'
                    QualityGateStatus(SonarQubecredentialsId)
                }
            }
        }

        stage ("Maven Build") {
        when {expression {params.action == 'Create'} }
            steps {
                script {
                    mvnBuild()
                }
            }
        }

        stage('Docker Image Build'){
         when { expression {  params.action == 'Create' } }
            steps{
               script{
                   
                   dockerBuild("${params.imageName}","${params.imageTag}","${params.dockerHub}")
               }
            }
        }
    }
}
