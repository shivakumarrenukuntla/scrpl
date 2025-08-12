node('Built-in')
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

