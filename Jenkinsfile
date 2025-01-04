node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'loubna-ka')]) {
                    // Configurer l'utilisateur Git
                    sh "git config user.email 'loubnakarim2001@gmail.com'"
                    sh "git config user.name 'loubna-ka'"

                    // Afficher le fichier deployment.yml avant modification
                    sh "cat deployment.yml"

                    // Remplacer l'image dans le fichier deployment.yml avec le DOCKERTAG
                    sh "sed -i 's+loubnakarim2001268/jenkins-flask.*+loubnakarim2001268/jenkins-flask:${DOCKERTAG}+g' deployment.yml"

                    // Afficher le fichier deployment.yml après modification
                    sh "cat deployment.yml"

                    // Ajouter les changements à Git
                    sh "git add ."

                    // Commiter les changements
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"

                    // Pousser les changements sur GitHub avec authentification
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/pfs-repo-2.git HEAD:main"
                }
            }
        }
    }
}
