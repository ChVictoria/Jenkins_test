pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://git.comsys.kpi.ua/student075/Lab4_IT', credentialsId: '50960055a9850bb153d88d64ec5bb1d812e52f53'
            }
        }
        
        stage('Build') {
            steps {
                // Крок для збірки проекту з Visual Studio
                // Встановіть правильні шляхи до рішення/проекту та параметри MSBuild
                bat '"path to MSBuild" Lab4_IT.sln /t:Build /p:Configuration=Release'
            }
        }

        stage('Test') {
            steps {
                // Команди для запуску тестів
                bat "x64\\Debug\\Lab4_IT.exe --gtest_output=xml:test_report.xml"
            }
        }
    }

    post {
    always {
        // Publish test results using the junit step
         // Specify the path to the XML test result files
    }
}
}