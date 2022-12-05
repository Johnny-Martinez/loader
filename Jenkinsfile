def imageName = 'mlabouardy/movies-loader'
node('workers'){
    stage('Checkout'){
        checkout scm
    }

    stage('Unit Tests'){
        def imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")
        imageTest.inside{
            sh "pwd"
            sh "python test_main.py"
            sh "pwd"
            sh "docker cp $WORKSPACE"
            junit "${env.WORKSPACE}/reports/*.xml"
        }
    }
}

def commitID() {
    sh 'git rev-parse HEAD > .git/commitID'
    def commitID = readFile('.git/commitID').trim()
    sh 'rm .git/commitID'
    commitID
}
