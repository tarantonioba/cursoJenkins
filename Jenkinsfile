pipeline{
    agent any
    stages{
        stage('Repositorio'){
            steps{
                echo 'Clono el repo'
                buildName '@BUILD_${BUILD_TIMESTAMP}_${BUILD_NUMBER}'
                git branch: 'desarrollo', url: 'https://github.com/tarantonioba/cursoJenkins.git'
            }
        }
        stage('Empaquetado'){
            steps{
                echo 'Lo hago con maven'
                sh 'cd miproyecto;mvn package'
            }
        }
        stage('Sonarqube'){
            steps{
                echo 'Llamo a sonar con maven'
                sh '''
                cd miproyecto
                
                mvn sonar:sonar -Dsonar.projectKey=curso \\
                  -Dsonar.host.url=http://172.31.3.49:8081 \\
                  -Dsonar.login=73e9fe1a21cdccc701e33947c0e78649dc396c0b
                '''
            }
        }
    }
post{
        always{
            echo 'Yo me ejecuto siempre'
        }
        success{
            echo 'Yo me ejecuto cuando todo ha ido bien'
            junit 'miproyecto/target/surefire-reports/*.xml'
            buildName '@BUILD_${BUILD_TIMESTAMP}_${BUILD_NUMBER}_OK'
            archiveArtifacts artifacts: 'miproyecto/target/*.jar', followSymlinks: false
        }
        failure{
            echo 'Yo me ejecuto cuando ha ido mal'
            buildName '@BUILD_${BUILD_TIMESTAMP}_${BUILD_NUMBER}_KO'
        }
        changed{
            echo 'Yo me ejecuto si esta ejecución no acaba en el mismo estado que la anterior ejecucion'
        }
    }
}