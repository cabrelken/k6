pipeline {
    agent {
        docker {
            image "grafana/k6"
            args "--entrypoint=''"
        }
    }

    parameters {
        string(name: 'TEMPS_STAGE_1', defaultValue: '1m', description: 'Choisir le temps stage 1')
        string(name: 'CHARGE_STAGE_1', defaultValue: '200', description: 'Choisir la charge stage 1')

        string(name: 'TEMPS_STAGE_2', defaultValue: '2m', description: 'Choisir le temps stage 2')
        string(name: 'CHARGE_STAGE_2', defaultValue: '200', description: 'Choisir la charge stage 2')

        string(name: 'TEMPS_STAGE_3', defaultValue: '300s', description: 'Choisir le temps stage 3')
        string(name: 'CHARGE_STAGE_3', defaultValue: '0', description: 'Choisir la charge stage 3')
    }

    stages {
        stage('Afficher les paramètres') {
            steps {
                echo "Paramètres utilisés:"
                echo "TEMPS_STAGE_1: ${params.TEMPS_STAGE_1}"
                echo "CHARGE_STAGE_1: ${params.CHARGE_STAGE_1}"
                echo "TEMPS_STAGE_2: ${params.TEMPS_STAGE_2}"
                echo "CHARGE_STAGE_2: ${params.CHARGE_STAGE_2}"
                echo "TEMPS_STAGE_3: ${params.TEMPS_STAGE_3}"
                echo "CHARGE_STAGE_3: ${params.CHARGE_STAGE_3}"
            }
        }

        stage('version de k6') {
            steps {
                sh 'k6 -v'
            }
        }

        stage('run test') {
            steps {
                sh """
                k6 run --stage ${params.TEMPS_STAGE_1}:${params.CHARGE_STAGE_1} \
                --stage ${params.TEMPS_STAGE_2}:${params.CHARGE_STAGE_2} \
                --stage ${params.TEMPS_STAGE_3}:${params.CHARGE_STAGE_3} collectionGrafana.postman_collection.json
                """
            }
        }
    }
}
