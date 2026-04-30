pipeline {
    agent any
    
    tools {
        // No additional tools needed for static website
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                echo '📦 Pulling latest code from GitHub...'
                git branch: 'main', 
                    url: 'https://github.com/your-username/my-static-website.git'
                echo '✅ Code pulled successfully!'
            }
        }
        
        stage('Validate HTML') {
            steps {
                echo '🔍 Validating HTML files...'
                sh '''
                    if [ -f "index.html" ]; then
                        echo "✅ index.html found"
                    else
                        echo "❌ index.html missing!"
                        exit 1
                    fi
                '''
            }
        }
        
        stage('Prepare Deployment') {
            steps {
                echo '📁 Preparing files for deployment...'
                sh '''
                    # Create backup of existing deployment
                    if [ -d "/var/www/html-backup" ]; then
                        sudo rm -rf /var/www/html-backup
                    fi
                    
                    if [ -d "/var/www/html" ]; then
                        sudo cp -r /var/www/html /var/www/html-backup
                        echo "✅ Backup created at /var/www/html-backup"
                    fi
                '''
            }
        }
        
        stage('Deploy to Nginx') {
            steps {
                echo '🚀 Deploying website to Nginx...'
                sh '''
                    # Copy all files to web directory
                    sudo cp -r * /var/www/html/
                    
                    # Set correct permissions
                    sudo chmod -R 755 /var/www/html/
                    
                    # Restart Nginx to apply changes
                    sudo systemctl reload nginx
                '''
                echo '✅ Deployment complete!'
            }
        }
        
        stage('Verify Deployment') {
            steps {
                echo '🔍 Verifying deployment...'
                sh '''
                    # Check if Nginx is running
                    if systemctl is-active --quiet nginx; then
                        echo "✅ Nginx is running"
                    else
                        echo "❌ Nginx is not running"
                        exit 1
                    fi
                    
                    # Check if website is accessible
                    curl -s -o /dev/null -w "%{http_code}" http://localhost/ | grep -q "200"
                    if [ $? -eq 0 ]; then
                        echo "✅ Website is accessible (HTTP 200)"
                    else
                        echo "❌ Website not accessible"
                        exit 1
                    fi
                '''
            }
        }
    }
    
    post {
        success {
            echo '🎉 PIPELINE SUCCESS! Website deployed successfully.'
            echo '🌐 Access at: http://' + env.NODE_NAME
        }
        failure {
            echo '❌ PIPELINE FAILED! Check the logs above.'
            echo '🔄 Rolling back to previous version...'
            sh '''
                if [ -d "/var/www/html-backup" ]; then
                    sudo rm -rf /var/www/html
                    sudo mv /var/www/html-backup /var/www/html
                    sudo systemctl reload nginx
                    echo "✅ Rollback complete"
                fi
            '''
        }
        always {
            echo '🏁 Pipeline finished at: ' + new Date().toString()
            // Clean up workspace
            cleanWs()
        }
    }
}
