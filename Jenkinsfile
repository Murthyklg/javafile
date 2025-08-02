pipeline {
    agent any

    tools {
        // Install the Maven version configured as "maven" and add it to the path.
        maven "maveninstall"
    }
    stages {
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/Murthyklg/javafile'
                sh "mvn clean package"
               
            }

           
        }
    }
    post {
        always {
            script {
                def jobName = env.JOB_NAME
                def buildNumber = env.BUILD_NUMBER
                def buildUrl = env.BUILD_URL
                def pipelineStatus = currentBuild.currentResult
                def bannerColor = pipelineStatus == 'SUCCESS' ? 'green' : 'red'

                def body = """
                    <html>
                    <body>
                    <div style="border: 4px solid ${bannerColor}; padding: 10px;">
                        <h2>${jobName} - Build #${buildNumber}</h2>
                        <div style="background-color: ${bannerColor}; padding: 10px;">
                            <h3 style="color: white;">Pipeline Status: ${pipelineStatus}</h3>
                        </div>
                        <p>Check the <a href="${buildUrl}">console output</a>.</p>
                    </div>
                    </body>
                    </html>
                """

                echo "Sending email..."
                emailext (
                    subject: "${jobName} - Build #${buildNumber} - ${pipelineStatus}",
                    body: body,
                    to: 'webdevmurthy@gmail.com',
                    from: 'murthyklg2711@gmail.com',
                    replyTo: 'murthyklg2711@gmail.com',
                    mimeType: 'text/html'
                )
            }
        }
    }
}
