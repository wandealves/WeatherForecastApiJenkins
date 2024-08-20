pipeline{
  agent any

  stages{
    stage('Checkout do código'){
      steps{
        git url :'https://github.com/wandealves/WeatherForecastApiJenkins.git', branch: 'main'
        sh 'ls -la'
      }
    }
  }
}