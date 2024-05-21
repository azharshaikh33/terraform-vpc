pipeline {
    agent any
    parameters {
        choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Select the environment') 
        choice(name: 'ACTION', choices: ['apply', 'destroy'], description: 'Select if you want to apply or destroy')
        }

    options {
        ansiColor('xterm')
    }
    stages {
        stage('terraform init') {
            steps {
                sh "terrafile -f env-dev/Terrafile"
                sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars"
            }
        }
        stage('terraform plan') {
            steps {
                sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
            }
        }
        stage('terraform apply') {
            steps {
                sh "terraform ${ACTION} -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
            }
        }
    }
}



