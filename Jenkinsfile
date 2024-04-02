pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://git.comsys.kpi.ua/student075/Lab4_IT', credentialsId: 'gitea_token'
            }
        }
        
        stage('Build') {
            steps {
                // Крок для збірки проекту з Visual Studio
                // Встановіть правильні шляхи до рішення/проекту та параметри MSBuild
                bat "\"${tool 'VS_build'}\\MSBuild.exe\" Lab4_IT.sln /t:Build /p:Configuration=Release"
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
			xunit (
				thresholds: [ skipped(failureThreshold: '0'), failed(failureThreshold: '0') ],
				tools: [ GoogleTest(pattern: 'test_report.xml') ]
			)
		}
	}
}