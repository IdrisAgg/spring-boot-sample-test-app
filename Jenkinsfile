pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'build stage'
        bat 'mvn -DskipTests clean package'
      }
    }

    stage('test') {
      parallel {
        stage('test') {
          steps {
            echo 'test d\'intégration'
          }
        }

        stage('test fonctionnel ') {
          steps {
            echo 'test fonctionnel '
          }
        }

        stage('smoke test') {
          steps {
            echo 'smoke test'
          }
        }

      }
    }

    stage('deploy') {
      steps {
        echo 'deploy'
      }
    }

  }
}