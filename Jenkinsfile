pipeline {
  tools {nodejs "node12"}

  environment {
    SENTRY_AUTH_TOKEN = credentials('sentry-auth-token')
    SENTRY_ORG = 'tae-company'
    SENTRY_PROJECT = 'setrytest'
    SENTRY_ENVIRONMENT = 'production'
  }

  stages {
    stage('Example') {
      steps {
        // Install Sentry CLI
        sh '''
          npm install
          export SENTRY_RELEASE=$(date +"%y-%m-%d")
          sentry-cli releases new -p $SENTRY_PROJECT $SENTRY_RELEASE
          sentry-cli releases set-commits $SENTRY_RELEASE --auto
          sentry-cli releases files $SENTRY_RELEASE upload-sourcemaps path-to-sourcemaps-if-applicable
          sentry-cli releases finalize $SENTRY_RELEASE
          sentry-cli releases deploys $SENTRY_RELEASE new -e $SENTRY_ENVIRONMENT
        '''
      }
    }
  }
}