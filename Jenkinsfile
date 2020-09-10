node {
  env.NODEJS_HOME = "${tool 'node12'}"
  env.PATH="${env.NODEJS_HOME}/bin:${env.PATH}"

  stage('Sentry') {
    // Install Sentry CLI
    sh 'npm install'
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