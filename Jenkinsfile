pipeline {
agent any

environment {
APP_ID = "YOUR-APPLICATION-ID"
}

parameters {
string(name: 'DEPLOY_URL_CRED_ID', defaultValue: 'DEPLOY_URL', description: 'Credentials ID for the deployment URL (Secret Text)')
string(name: 'DEPLOY_KEY_CRED_ID', defaultValue: 'DEPLOY_KEY', description: 'Credentials ID for the deployment API key (Secret Text)')
string(name: 'VITE_CANDIDATES_ENDPOINT', defaultValue: 'VITE_CANDIDATES_ENDPOINT', description: 'Endpoint for candidates API used by the frontend (exported into .env)')
}

stages {
stage('Checkout') {
steps {
checkout scm
}
}

stage('Setup .env') {
  steps {
    sh "echo 'VITE_CANDIDATES_ENDPOINT=${params.VITE_CANDIDATES_ENDPOINT}' > .env"
    sh 'echo ".env created with VITE_CANDIDATES_ENDPOINT"'
  }
}

stage('Install dependencies') {
  steps {
    sh 'node -v && npm --version && (npm ci || npm install)'
  }
}

// Skipping explicit install of test libraries because they are already in devDependencies

stage('Run tests') {
  steps {
    sh 'npm test -- --run'
  }
}
