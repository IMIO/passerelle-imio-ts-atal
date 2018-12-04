pipeline {
    agent any
    triggers {
        pollSCM('*/3 * * * *')
    }
    options {
        // Keep the 50 most recent builds
        buildDiscarder(logRotator(numToKeepStr:'50'))
    }
    stages {
        stage('Build') {
            steps {
                sh "fpm -n passerelle-imio-ts-atal -s python -t deb -v `cat version` --prefix /usr -d passerelle setup.py"
            }
        }
        stage('Deploy') {
            steps {
                sh "scp passerelle-imio-ts-atal_`cat version`_all.deb root@puppetmaster.imio.be:/tmp"
            }
        }
    }
}
