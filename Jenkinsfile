def imageName = 'johnnym/movies-loader'
node('workers') {
    stage('Checkout') {
        checkout scm
    }

    stage('Unit Tests') {
        def imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")
        imageTest.inside {
            sh "python test_main.py"
            sh 'pwd'
            junit "**/reports/*.xml"
        }
    }
}

def commitID() {
    sh 'git rev-parse HEAD > .git/commitID'
    def commitID = readFile('.git/commitID').trim()
    sh 'rm .git/commitID'
    commitID
}
