pipeline {
agent any

```
stages {

    stage('Checkout') {
        steps {
            git branch: 'main',
                url: 'https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git'
        }
    }

    stage('Deploy to IIS') {
        steps {
            bat '''
                echo Deploying application to IIS...

                if not exist "C:\\inetpub\\wwwroot\\jenkins-iis-demo" (
                    mkdir "C:\\inetpub\\wwwroot\\jenkins-iis-demo"
                )

                copy /Y "index.html" "C:\\inetpub\\wwwroot\\jenkins-iis-demo\\index.html"

                echo Deployment completed successfully.
            '''
        }
    }

    stage('Verify Deployment') {
        steps {
            bat '''
                if exist "C:\\inetpub\\wwwroot\\jenkins-iis-demo\\index.html" (
                    echo index.html exists in IIS web root.
                ) else (
                    echo ERROR: index.html was not deployed.
                    exit /b 1
                )
            '''
        }
    }
}

post {
    success {
        echo 'IIS deployment successful!'
    }

    failure {
        echo 'IIS deployment failed!'
    }
}
```

}
