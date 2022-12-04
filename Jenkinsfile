def imageName = 'johnnym/movies-loader'
node('workers'){
    stage('Checkout'){
        checkout scm
    }
    stage('Unit Tests') {
        sh "docker build -t ${imageName}-test -f Dockerfile.test ."
        sh "docker run --rm ${imageName}-test"
    }
}

def commitID() {
    sh 'git rev-parse HEAD > .git/commitID'
    def commitID = readFile('.git/commitID').trim()
    sh 'rm .git/commitID'
    commitID
}