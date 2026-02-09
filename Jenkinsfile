pipeline {
    agent any

    stages {

        stage('Install Nginx (Windows)') {
            steps {
                powershell '''
                $version = "1.27.4"
                $url = "https://nginx.org/download/nginx-$version.zip"
                $zip = "C:\\nginx.zip"

                if (!(Test-Path "C:\\nginx")) {
                    Invoke-WebRequest -Uri $url -OutFile $zip
                    Expand-Archive $zip -DestinationPath C:\\
                    Rename-Item "C:\\nginx-$version" nginx
                }
                '''
            }
        }

        stage('Deploy Config & HTML') {
            steps {
                powershell '''
                Stop-Process -Name nginx -ErrorAction SilentlyContinue
                Copy-Item ".\\nginx.conf" "C:\\nginx\\conf\\nginx.conf" -Force
                Copy-Item ".\\html\\*" "C:\\nginx\\html" -Recurse -Force
                '''
            }
        }

        stage('Start Nginx') {
            steps {
                powershell '''
                Start-Process "C:\\nginx\\nginx.exe"
                '''
            }
        }
    }
}
