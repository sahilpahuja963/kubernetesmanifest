node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email sahilpahuja963@gmail.com"
                        sh "git config user.name SahilPahuja"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+sahilpahuja963/test.*+sahilpahuja963/test:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push git@github.com:${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
      }
    }
  }
}
}
