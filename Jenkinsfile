node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                   // for prod or no showcase the project: use:  variable: 'GITHUB_TOKEN'   is recommended
                   //passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME'
                    withCredentials([usernamePassword(credentialsId: 'github-id', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME' )]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email arthus8ni@gmail.com"
                        sh "git config user.name Arthus"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+22nit/flaskcicd.*+22nit/flaskcicd:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        //sh "git push https://${GITHUB_TOKEN}@github.com/Tusartus/aks-flaskmanifestargocd.git HEAD:main"
                         sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
                     }
                 }
             
            }

    }





}
