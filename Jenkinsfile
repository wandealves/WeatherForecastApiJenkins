pipeline{
  agent any

  stages{
    stage('Checkout do código'){
      steps{
        git url :'https://github.com/wandealves/WeatherForecastApiJenkins.git', branch: 'main'
        
      }
    }

    stage('Construção da imagem Docker'){
      steps{
        script{
          dockerapp = docker.build("wandersonalves/weather-forecast-api:${env.BUILD_ID}", ' .')
        }
      }
    }

    stage('Publicação da imagem Docker'){
      steps{
        script{
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub'){
            dockerapp.push('latest')
            dockerapp.push("${env.BUILD_ID}")
          }
        }
      }
    }

    stage('Limpeza'){
      steps{
        script{
           dockerapp.clean()
        }
      }
    }
  }
}