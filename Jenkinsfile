pipeline {
    agent any // Runs on any available agent; specify a label if necessary
    tools {
        terraform 'Terraform' // Ensure Terraform is configured under "Manage Jenkins > Global Tool Configuration"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', credentialsId: 'token-terraform', url: 'https://github.com/Lalitha891/terraform-repo.git'           }
        }
        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }
        stage('Terraform Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }
        stage('Terraform Apply') {
            steps {
                sh 'terraform apply -auto-approve tfplan'
            }
        }
        stage('Verify File Creation') {
            steps {
                sh 'ls -l $WORKSPACE/pets.txt || echo "File not found!"'
                sh 'cat $WORKSPACE/pets.txt || echo "No content!"'
            }
        }
    }
}
