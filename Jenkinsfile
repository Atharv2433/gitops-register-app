pipeline {
    agent { label "Jenkins-agent" }
    environment {
              APP_NAME = "demo"
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM") {
               steps {
                   git branch: 'main', credentialsId: 'github', url: 'https://github.com/Atharv2433/gitops-register-app'
               }
        }

        stage("Update the Deployment Tags") {
            steps {
                sh """
                   cat deployment.yaml
                   sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                   cat deployment.yaml
                """
            }
        }

        stage("Push the changed deployment file to Git") {
            steps {
                sh """
                   git config --global user.name "Atharv2433"
                   git config --global user.email "atharvjoundal@gmail.com"
                   git add deployment.yaml
                   git commit -m "Updated Deployment Manifest"
                """
                    withCredentials([usernamePassword(credentialsId: 'github', usernameVariable: 'Atharv2433', passwordVariable: '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')]) {
                        sh "git push https://Atharv2433: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@github.com/Atharv2433/gitops-register-app.git main"
                    }

            }
        }
      
    }
}
