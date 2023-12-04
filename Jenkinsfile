pipeline {
    agent { label 'DOTNET' }
    triggers {
        pollSCM('* * * * 1-5')
    }
    stages {
        stage('git') {
            steps {
                git url: 'https://github.com/dummyrepos/nopCommerceNov23.git',
                    branch: 'develop'
            }
        }
        stage('build') {
            steps {
                sh 'dotnet build -c Release src/NopCommerce.sln'
                sh 'dotnet publish -c Release src/Presentation/Nop.Web/Nop.Web.csproj  -o "./published" '

            }
            post {
                success {
                    sh 'mkdir ./published/bin ./published/logs'
                    sh 'tar -czvf nop.web.tar.gz ./published/'
                    archiveArtifacts '**/*.tar.gz'
                }
            }
        }
    }
}