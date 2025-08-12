node('master')
{
    stage('ContinuousDownload') 
    {
         git 'https://github.com/shivakumarrenukuntla/spl.git'
    }
    stage('ContinuousBuild') 
    {
         sh label: '', script: 'mvn package'
    }
    
    
}

