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
    }
}
