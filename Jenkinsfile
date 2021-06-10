pipeline {
    agent any
    environment {
        // list all environmental variables
        VERSION_NO = '1.0'
        // credentials('test-cred') finds the credential name from Jenkins
        SECRETS = credentials('test-cred')
    }

    tools {
        // Jankins supports 3 build tools, maven, jdk and gradle 
        maven "Maven"
    }

    parameters {
        string(name: 'VERSION', defaultValue: '1.01', description: 'Version umber')
        choice(name: 'VERSION_TAGS', choices: ['js', 'ts', 'cs', 'ns'], description: 'version tags array')
        booleanParam(name: 'BUILDS', defaultValue: true, description: 'Builds feedback')
    }
    stages {
        stage('build') {
            steps {
                echo "building veriosn ${VERSION_NO}...."
                echo "version tags ${params.VERSION_TAGS}...."
            }
        }

        stage('test') {
            // add a when block jsst if block
            // when {
            //     expression {
            //         BRANCH_NAME == 'dev'
            //     }
            // }
            steps {
                echo "testing with ${SECRETS}...."
                // you can also use it inline with withCredentials func
                // objects are defined using []
                withCredentials([
                    usernamePassword(credentials: 'test-cred', usernameVariable: USER, passwordVariable: PASSWORD)
                ]) {
                    sh "some script ${USER} and ${PASSWORD}"
                }
            }
        }
    }
}

// Go to http://localhost:8080/env-vars.html/ to get list of commands provided by Jenkins