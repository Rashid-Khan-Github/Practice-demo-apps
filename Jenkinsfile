def gv

pipeline {
    agent any
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }

    stages {
        
        stage("init"){
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        
        stage("Build") {
            steps {
                script {
                    gv.buildApp()
                }
            }
        }
        
        stage("Test") {
            when {
                expression {
                    params.executeTests
                }
            }
            steps {
                script {
                    gv.testApp()
                }
            }
        }

        stage("deploy") {
            input{
                message "Select the Environment to Deploy"
                ok "Select"
                parameters{
                    choice(name: 'FIRST', choices: ['dev', 'staging', 'prod'], description: '')
                    choice(name: 'SECOND', choices: ['dev', 'staging', 'prod'], description: '')
                }
            }
            steps {
                script {
                    gv.deployApp()
                    echo "Deploying to ${FIRST}"
                    echo "Deploying to ${SECOND}"
                }
            }

        }
        
    }
}
