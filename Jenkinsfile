def groo_sc

pipeline {
    agent any
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: 'for you choice')
    }
    stages {
        stage("Loading Script..."){
            steps{
                script{
                    groo_sc = load "script.groovy"
                }
            }
        }
        stage("Build") {
            steps {
                script{
                    groo_sc.buildApp()
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
                script{
                    groo_sc.testApp()
                }
            }
        }

        
        stage("deploy") {
            steps {
                script{
                    groo_sc.deployApp()
                }
            }

        }
    }
}