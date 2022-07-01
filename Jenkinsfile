pipeline {
    agent any 
    environment {
       DOCKER = tool 'docker' 
       DOCKER_EXEC = '$DOCKER/docker'
       SCA = '/Users/user/Documents/dependency-check/bin/dependency-check.sh'
       TRIVY = '/Users/user/Documents/trivy_0.29.2_macOS-64bit/trivy'
       SONARKEY = ''
    }
    stages {
      
      stage('SCM') {
         steps {
            figlet 'SCM'
            checkout scm // clonacion de codigo en nodo
         }
      }
        
      stage('SAST') {
         steps {
            withCredentials([string(credentialsId: 'sonarcloud', variable: 'SONARPAT')]) {
                 figlet 'SAST'
                 sh('set +x; ./gradlew sonarqube -Dsonar.login=$SONARKEY -Dsonar.branch.name=feature-jenkins')
            }
         }
      }
        
//      stage('SCA') {
//        steps {
//            figlet 'SCA'
//            sh "$SCA --project 'spring-clinic' --scan '${WORKSPACE}/build/libs/pet-clinic-2.6.0.jar'"
//            echo '************** SBOM CYCLONEDX **************'
//            sh "./gradlew cyclonedxBom -info"
//        }
//     }
     
        
   }
}

