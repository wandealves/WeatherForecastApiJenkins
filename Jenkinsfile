pipeline{
  agent any

  stages{
    stage('Checkout do código'){
      steps{
        git url :'https://github.com/wandealves/WeatherForecastApiJenkins.git', branch: 'main'
        
      }
    }

  stage('Executar o docker-compose down'){
    steps{
      // Certifique-se de que o arquivo docker-compose.yml está no diretório correto
      sh 'docker compose down'
    }
  }

  stage('Remover a imagem latest Docker'){
    steps{
      sh 'docker rmi wandersonalves/weather-forecast-api:latest -f'
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

    stage('Executar o docker-compose up'){
      steps{
            // Certifique-se de que o arquivo docker-compose.yml está no diretório correto
            sh 'docker compose up --build -d'
      }
    }

  }
}