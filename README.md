# ci-cd-webapp
LAB EXERCISE – 10

## Applying CI/CD Principles to Web Development Using Jenkins, Git, using Docker Containers

PROCEDURE:
Step 1: Set Up the Web Application and Git Repository
Create a simple web application or use an existing one. Ensure it can be
hosted in a Docker container.
Initialise a Git repository for your web application and push it to GitHub.

Step 2: Install and Configure Jenkins
Install Jenkins on your computer or server following the instructions for your operating system (https://www.jenkins.io/download/).
Open Jenkins in your web browser (usually at http://localhost:8080) and
complete the initial setup, including setting up an admin user and installing
necessary plugins.
Configure Jenkins to work with Git by setting up Git credentials in the Jenkins
Credential Manager.

Step 3: Create a Jenkins Job
    • Create a new Jenkins job using the "Freestyle project" type.
    • In the job configuration, specify a name for your job and choose "This project is parameterized."
    • Add a "String Parameter" named GIT_REPO_URL and set its default value to your Git repository URL.
    • Set Branches to build -> Branch Specifier to the working Git branch (ex*/master)
    • In the job configuration, go to the "Build Triggers" section and select the
    • "GitHub hook trigger for GITScm polling" option. This enables Jenkins to
    • listen for GitHub webhook triggers.
    
Step 4: Configure Build Steps
In the job configuration, go to the "Build" section.
Add build steps to execute Docker commands for building and deploying the
containerized web application. Use the following commands:
# Remove the existing container if it exists
docker rm --force container1
# Build a new Docker image
docker build -t nginx-image1 .
# Run the Docker container
docker run -d -p 8081:80 --name=container1 nginx-image1
These commands remove the existing container (if any), build a Docker
image named "nginx-image1," and run a Docker container named
"container1" on port 8081.

Step 5: Set Up a GitHub Webhook
In your GitHub repository, navigate to "Settings" and then "Webhooks."
[Create a new webhook, and configure it to send a payload to the Jenkins
webhook URL (usually http://jenkins-server/github-webhook/). Set the content
type to "application/json."

Step 6: Trigger the CI/CD Pipeline
Push changes to your GitHub repository. The webhook will trigger the Jenkins
job automatically, executing the build and deployment steps defined in the job
configuration.
Monitor the Jenkins job's progress in the Jenkins web interface.

Step 7: Verify the Deployment
Access your web application by opening a web browser and navigating to
http://localhost:8081 (or the appropriate URL if hosted elsewhere).
