node('php'){
    stage('Clean'){
        deleteDir()
        sh 'ls -la'
    }
    
    stage('Fetch') {
        checkout scm
    }
    
    stage('Build'){
        sh 'composer install --prefer-dist --no-scripts --no-dev --ignore-platform-reqs'
    }
    
    stage('config') {
        parallel(
            'config cache': {
                echo 'tarefa paralela 1'
            },
            'config route': {
                echo 'tarefa paralela 2'
            }
        )
    }
    stage('Docker Build') {
        sh 'docker build -t marcelonunes/laravel:$BUILD_NUMBER .'
    }
    
    stage('Docker Ship') {
        sh 'docker push marcelonunes/laravel:$BUILD_NUMBER'
    }
}
