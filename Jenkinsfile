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
          dockerapp = docker.build("wandersonalves/weather-forecast-api:${env.BUILD_ID}", '-f ./Dockerfile .')
        }
      }
    }
  }
}