pipeline{
    agent any
    stages{
        stage('Repositorio'){
            steps{
                echo 'Clonamos el repositorio'
                git url: 'https://github.com/tarantonioba/cursoJenkins/tree/desarrollo/miproyecto'
            }
        }
        stage('Empaquetado'){
            steps{
                echo 'Empaquetado mediante MAVEN'
                sh 'mvn package'
            }
        
    }
    post{
        always{
            echo 'ejecuto siempre'
        }
        success{
            echo 'ejecuto si va bien'
        }
        failure{
            echo 'ejecuto cuando ha ido mal'
        }
        changed{
            echo 'ejecuto si esta ejecución no acaba en el mismo estado que la anterior ejecucion'
        }

    }
}