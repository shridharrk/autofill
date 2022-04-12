pipeline {
    agent any

    stages {
        stage ('Stage 1') {
            steps {
                echo "First stage OK"
            }
        }
        stage('Wait on Webhook') {
            options {
                timeout(time: 2, unit: "MINUTES")
            }
            steps {
                script {
                    hook = registerWebhook()
                    callbackURL = hook.url
                    
                    // Call a remote system to start execution, passing the callback url
                    //sh "curl -X POST -H 'Content-Type: application/json' -d '{\"callback\":\"${callbackURL}"}' http://httpbin.org/post"

                    echo "Waiting for POST to ${callbackURL}"
                    data = waitForWebhook hook
                    
                    echo "Webhook called with data: ${data}"
                }
            }
        }
        stage('last stage') {
            steps {
                echo "Done!"
            }
        }
    }
}
