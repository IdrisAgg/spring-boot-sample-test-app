pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'build stage'
        bat 'mvn -DskipTests clean package'
        archiveArtifacts '**/target/*.jar'
      }
    }

    stage('test') {
      parallel {
        stage('smoke') {
          steps {
            echo 'test d\'intégration'
            bat 'mvn -Dtest="com.example.testingweb.smoke.**" test'
            junit '**/target/surefire-reports/TEST-*.xml'
          }
        }

        stage('Integration') {
          steps {
            echo 'test fonctionnel '
            bat 'mvn -Dtest="com.example.testingweb.integration.**" test'
          }
        }

        stage('Functional') {
          steps {
            echo 'smoke test'
            bat 'mvn -Dtest="com.example.testingweb.functional.**" test'
          }
        }

      }
    }

    stage('deploy') {
      steps {
        input 'Voulez vous continuer ?'
        echo 'deploy'
        bat 'mvn -DskipTests install'
      }
    }

  }
}