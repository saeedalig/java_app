@Library("my-shared-lib") _

pipeline {

    agent any

    parameters {
        choice (name: 'action', choices: 'Create\nDelete', description: 'Choose Create/Destroy')
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
    }
}
