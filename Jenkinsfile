node {
    // Folder on the EC2 server where the website will be copied
    def appDir = '/var/www/TechnoTrends'

    stage('Clean Workspace') {
        echo 'Remove old files from the Jenkins workspace'
        deleteDir()
    }

    stage('Clone Repo') {
        echo 'Download the latest code from GitHub'
        git(
            branch: 'main',
            url: 'https://github.com/Marathe-Suraj/TechnoTrends.git'
        )
    }

    stage('Deploy') {
        echo 'Copy the website files to the server folder'
        sh """
            # Create the folder if it does not exist
            sudo mkdir -p ${appDir}

            # Give Jenkins permission to write into that folder
            sudo chown -R jenkins:jenkins ${appDir}

            # Copy project files into the deploy folder
            # --delete removes old files that are no longer in the repo
            rsync -av --delete --exclude='.git' ./ ${appDir}/

            # Give the web server permission to read the files
            sudo chown -R www-data:www-data ${appDir}
        """
    }
}
