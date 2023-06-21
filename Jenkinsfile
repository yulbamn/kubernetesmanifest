node {
    def app

    stage('Clone repository') {     
        checkout scm
    }

    stage('Update GIT') {
            script {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh "git config user.email yulbamn@gmail.com"
                        sh "git config user.name yulbamn"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+zenaksacr.azurecr.io/shopping-web.*+zenaksacr.azurecr.io/shopping-web:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${DOCKERTAG}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
                    }
                
            }
    }
}
