node {
        def  SENTRY_AUTH_TOKEN = credentials('sentry-auth-token')
      def SENTRY_ORG = 'tae-company'
      def SENTRY_PROJECT = 'nodejs'
      def SENTRY_ENVIRONMENT = 'production'

  stage('Sentry') {

  // Install Sentry CLI
                sh 'curl -sL https://sentry.io/get-cli/ --no-clobber | bash'
  sh '''
      export SENTRY_RELEASE=$(date +"%y-%m-%d")
      sentry-cli releases new -p $SENTRY_PROJECT $SENTRY_RELEASE
      sentry-cli releases set-commits $SENTRY_RELEASE --auto
      sentry-cli releases files $SENTRY_RELEASE upload-sourcemaps path-to-sourcemaps-if-applicable
      sentry-cli releases finalize $SENTRY_RELEASE
      sentry-cli releases deploys $SENTRY_RELEASE new -e $SENTRY_ENVIRONMENT
    '''
  }
}