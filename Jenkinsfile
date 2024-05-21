pipeline {
    agent any
    parameters { choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Select the environment') }
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
                sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
            }
        }
    }
}


