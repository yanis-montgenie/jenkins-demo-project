// Jenkinsfile
@Library('ma-lib-partagee') _

pipeline {
    agent any

    stages {
        stage('Utiliser MonUtilitaire') {
            steps {
                script { // Ce bloc script est déjà présent, c'est bien.
                    org.exemple.utils.MonUtilitaire.saluer(this, "Jenkins User")
                    def messageSucces = org.exemple.utils.MonUtilitaire.genererMessage("succes")
                    echo messageSucces
                }
            }
        }

        stage('Utiliser autreFonction') {
            steps {
                // 'def resultat = ...' est une déclaration de variable Groovy,
                // et l'appel de 'autreFonction' est une étape que l'on veut capturer dans une variable.
                script {
                    def resultat = autreFonction("Ceci est un test de fonction globale.")
                    echo "Résultat de autreFonction : ${resultat}"
                }
            }
        }

        stage('Appeler monEtapePersonnalisee') {
            steps {
                // Le bloc 'monEtapePersonnalisee' contient déjà un 'script {}'
                // dans la Shared Library, mais pour l'appel à MonUtilitaire.saluer(this, ...)
                // il est prudent d'ajouter un 'script {}' autour de cet appel si vous le faites directement
                // à l'intérieur du bloc passé à monEtapePersonnalisee.
                // Cependant, la Shared Library gère déjà le contexte 'script' via 'body()'.
                // L'erreur suggère que le problème est plus à la racine de l'appel MonUtilitaire.saluer dans le Jenkinsfile.
                // Je pense que la ligne 33 est celle dans le bloc `monEtapePersonnalisee { ... }`.

                // Corrigeons comme ceci pour être sûr :
                monEtapePersonnalisee {
                    echo "Ceci est le contenu du bloc passé à monEtapePersonnalisee."
                    echo "On peut même appeler une fonction de la Shared Library ici :"
                    // Ici, l'appel à 'MonUtilitaire.saluer' doit être dans un 'script {}'
                    // car il n'est pas directement une étape de pipeline mais un appel de méthode Groovy
                    script {
                        org.exemple.utils.MonUtilitaire.saluer(this, "De l'interieur de l'etape personnalisee")
                    }
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline terminé."
        }
    }
}