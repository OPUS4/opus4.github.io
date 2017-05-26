#!groovy

pipeline {
    agent any

    stages {
        stage('prepare') {
            steps {
                writeFile([file: '_localconfig.yml', text: "baseurl: \"/jenkins/job/opus4home/job/${env.BRANCH_NAME}/OPUS_4_Home\""])
            }
        }

        stage('build') {
            steps {
                sh 'pwd'

                // install required bundles
                sh 'bundle install'

                // build documentation
                sh 'bundle exec jekyll build --config _config.yml,_localconfig.yml'
            }
        }

        stage('publish') {
            steps {
                publishHTML(target: [
                        allowMissing: false,
                        alwaysLinkToLastBuild: false,
                        keepAll: true,
                        reportDir: '_site/',
                        reportFiles: 'index.html',
                        reportName: 'OPUS 4 Home'
                ])
            }
        }
    }
}