pipeline {
    agent {
        label'master'
    }
    paraemters {
        choice(name: 'Environment', choices: ['dev', 'qa'], description: 'cft target Environment',)
        string(name: 'StackName', defaultValue: '', description: 'cft stackname',)
    }
    stages {
        stage('checkout scm') {
            steps {
                git branch: 'master',
                    credentialsId: 'github_jenkins',
                        url: 'https://github.com/oscarose/CFTenvironment.git'
            }
        }
        stage('deploy dev stack') {
            when {
                expression { params.Environment == 'dev' }
            }
            steps {
                sh """
                aws cloudformation create-stack --stack-name ${params.StackName} --template-body file://CFTenv.yaml --parameters ParameterKey=Environment,ParameterValue=dev --capabilities CAPABILITY_NAMED_IAM
                """
            }
        }
        stage('deploy qa stack') {
            when {
                expresssion { params.Environment == 'qa' }
            }
            steps {
                sh """
                aws cloudformation create-stack --stack-name ${params.StackName} --template-body file://CFTenv.yaml --parameters ParameterKey=Environment,ParameterValue=qa --capabilities CAPABILITY_NAMED_IAM
                """
            }
        }
    }
}
