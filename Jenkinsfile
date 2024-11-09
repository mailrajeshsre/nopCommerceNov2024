pipeline {
    agent { label 'DOTNET' }
    triggers {
       pollSCM('* * * * 1-5')
     }
     stages {
        stage('Git-Clone') {
           steps {
              git: url: 'https://github.com/mailrajeshsre/nopCommerceNov2024.git', branch: 'master'
          }
        }
        stage('Build the code' ) {
            steps {
                 sh 'dotnet build -c Release src/NopCommerce.sln'
                 sh 'dotnet publish -c Release src/Presentation/Nop.Web/Nop.Web.csproj -o "./published"'
           }
           post {
              success {
             //   sh 'mkdir ./published/bin ./published/logs'
                sh 'tar -czvf nop.web.tar.gz ./published/'
                archiveArtifacts '**/*.tar.gz'
           }
        }
      }
    }
}
