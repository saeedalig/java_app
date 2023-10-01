@Library("my_shared_library") _

pipeline {

    agent any 

    #parameters {
        #choice (name: 'action', choices: 'Create\nDelete', description: 'Choose Create/Destroy')
        #string (name: 'ImageName', description: "name of the docker build", defaultValue: 'java_app')
        #string (name: 'ImageTag', description: "tag of the docker build", defaultValue: 'v1')
        #string (name: 'DockerHubUser', description: "name of the Application", defaultValue: 'asa96')
    #}

    
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
    }
}
