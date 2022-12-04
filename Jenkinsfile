pipeline {
  agent any
    stages {
      stage('Build images and push them to Dockerhub') {
        steps {
          sh '''#!/usr/bin/env bash
            # Make Bash Great Again
            set -o errexit # exit when a command fails.
            set -o nounset # exit when using undeclared variables
            set -o pipefail # catch non-zero exit code in pipes
            # set -o xtrace # uncomment for bug hunting

            docker build -t webarchiv/vyvoj:naki .
            docker push webarchiv/vyvoj:naki
          '''
        }
      }
      stage('Deploy vyvoj to Test Environment: https://app.webarchiv.cz/vyvoj') {
        when {
          anyOf { branch 'main'; branch 'production'}
        }
        environment {
                SSH_CREDS = credentials('ansible')
        }
        steps {
          sh '''#!/usr/bin/env bash
            # Make Bash Great Again
            set -o errexit # exit when a command fails.
            set -o nounset # exit when using undeclared variables
            set -o pipefail # catch non-zero exit code in pipes
            # set -o xtrace # uncomment for bug hunting
            
            # Upcoming script is deployed via Seeder repository.
            ssh -o "StrictHostKeyChecking=no" -i ${SSH_CREDS} ${SSH_CREDS_USR}@10.3.0.110 sudo /home/ansible/seeder/update_vyvoj.sh
          '''
        }
      }
      stage('Deploy vyvoj to Production Environment: https://webarchiv.cz/vyvoj') {
        when {
          anyOf { branch 'production'}
        }
        environment {
                SSH_CREDS = credentials('ansible')
        }
        steps {
          input "Přísáhám před krutým a přísným bohem, že https://app.webarchiv.cz/vyvoj je v perfektním stavu a stvrzuji, že může jít do produkce na https://webarchiv.cz/vyvoj."
          sh '''#!/usr/bin/env bash
            # Make Bash Great Again
            set -o errexit # exit when a command fails.
            set -o nounset # exit when using undeclared variables
            set -o pipefail # catch non-zero exit code in pipes
            # set -o xtrace # uncomment for bug hunting

            ssh -o "StrictHostKeyChecking=no" -i ${SSH_CREDS} ${SSH_CREDS_USR}@10.3.0.50 sudo /home/ansible/seeder/update_vyvoj.sh
          '''
        }
      }      
    }
}
