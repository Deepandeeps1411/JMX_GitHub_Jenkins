pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Deepandeeps1411/JMX_GitHub_Jenkins.git'
            }
        }

        stage('Run JMeter Test') {
            steps {
                bat '''
                for %%f in ("%WORKSPACE%\\*.jmx") do (
                    "D:\\JMeter\\apache-jmeter-5.6.3\\bin\\jmeter.bat" -n -t "%%f" -l "%WORKSPACE%\\results.jtl" -e -o "%WORKSPACE%\\HTMLReport"
                )
                '''
            }
        }

        stage('Send Email') {
            steps {
                emailext(
                    subject: "JMeter Report - ${BUILD_NUMBER}",
                    body: """
Build completed.

Job URL:
${BUILD_URL}
                    """,
                    to: "deepanvinayagam1411@gmail.com",
                    attachmentsPattern: '**/HTMLReport/**'
                )
            }
        }
    }
}
