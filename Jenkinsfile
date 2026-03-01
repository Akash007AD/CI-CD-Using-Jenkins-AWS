node{
    def appDir = '/var/www/nextjs-app'

    stage('Clean Workspace') {
        deleteDir()
    }

    stage('Clone Repository') {
        git (
            branch: 'main',
            url: 'https://github.com/Akash007AD/CI-CD-Using-Jenkins-AWS.git'
        )
    }

    stage('Install Dependencies') {
        sh 'npm install'
    }

    stage('Deploy to AWS') {
        sh """
            sudo mkdir -p ${appDir}
            sudo chown -R \$USER:\$USER ${appDir}

            rsync -av --delete --exclude='node_modules' --exclude='.git' ./ ${appDir}/

            cd ${appDir}
            npm install
            npm run build
            sudo fuser -k 3000/tcp || true
            nohup npm run start > app.log 2>&1 &
        """
    }
}