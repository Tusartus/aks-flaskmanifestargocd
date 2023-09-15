node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
        environment {
            
            GIT_USERNAME = "Tusartus"
        }

      steps{
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                   // for prod or no showcase the project: use:  variable: 'GITHUB_TOKEN'   is recommended
                   //asswordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME'
                    withCredentials([usernamePassword(credentialsId: 'github',    variable: 'GITHUB_TOKEN' )]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email arthus8ni@gmail.com"
                        sh "git config user.name Arthus"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+22nit/flaskcicd.*+22nit/flaskcicd:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GITHUB_TOKEN}@github.com/${GIT_USERNAME}/aks-flaskmanifestargocd.git HEAD:main"
                     }
                 }
             }
       }

    }





}
