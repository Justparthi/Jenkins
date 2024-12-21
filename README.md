## CI/CD Pipeline with Jenkins

### Steps to Set Up a CI/CD Pipeline with Jenkins:

#### 1. **Install Jenkins**
   - **Install Jenkins on your server:**
     - For Ubuntu:

       ```bash
       sudo apt update
       sudo apt install openjdk-11-jdk
       wget -q -O - https://pkg.jenkins.io/keys/jenkins.io.key | sudo tee /etc/apt/trusted.gpg.d/jenkins.asc
       sudo sh -c 'echo deb http://pkg.jenkins.io/debian/ / > /etc/apt/sources.list.d/jenkins.list'
       sudo apt update
       sudo apt install jenkins
       ```

     - For macOS (using Homebrew):

       ```bash
       brew install jenkins-lts
       ```

   - **Start Jenkins:**

     ```bash
     sudo systemctl start jenkins
     sudo systemctl enable jenkins
     ```

     - Jenkins will be accessible by default at `http://localhost:8080`.

#### 2. **Unlock Jenkins**
   - Once Jenkins is running, navigate to `http://localhost:8080` in your web browser.
   - You will be prompted to unlock Jenkins. Get the unlock key from the following location:
   
     ```bash
     sudo cat /var/lib/jenkins/secrets/initialAdminPassword
     ```

   - Enter the key into the unlock page and follow the prompts to install recommended plugins and create an admin user.

#### 3. **Install Required Plugins**
   - Go to **Manage Jenkins** > **Manage Plugins**.
   - Install the following essential plugins:
     - Git plugin
     - Pipeline plugin
     - Docker (if you're using Docker for deployment)
     - Maven or Gradle plugin (if you're using Maven/Gradle for builds)

#### 4. **Create a Jenkins Pipeline**
   - From the Jenkins dashboard, click on **New Item**.
   - Choose **Pipeline** and give it a name (e.g., `my-app-pipeline`).
   - In the **Pipeline** section, choose **Pipeline script** and define your pipeline using the **Declarative Pipeline syntax** or **Scripted Pipeline syntax**.
### 5. **Linking the Repository**
   - Ensure that your repository is linked to Jenkins. In the **Checkout** step, the pipeline pulls code from GitHub using the URL you specify. Make sure you set up **GitHub credentials** if your repository is private.

### 6. **Trigger the Pipeline**
   - The pipeline can be triggered manually or automatically using webhooks from GitHub. For automatic triggers:
     - Go to **Manage Jenkins** > **Configure System** > **GitHub**.
     - Set up **GitHub Webhook** to trigger the pipeline on push events.

### 7. **Deploy the Application**
   - In the **Deploy** stage, add the necessary steps to deploy your application. This could involve SSH-ing into a server, pushing a Docker container, or using an AWS/Azure deployment script.

---

### GitHub Documentation Links:

- **Jenkins Documentation**:
  - [Jenkins Documentation](https://www.jenkins.io/doc/)
  - Specifically, for **Pipeline as Code**: [Pipeline Documentation](https://www.jenkins.io/doc/book/pipeline/)

- **GitHub Integration with Jenkins**:
  - [GitHub Plugin Documentation](https://plugins.jenkins.io/github/)
  - [GitHub Webhooks](https://docs.github.com/en/developers/webhooks-and-events/webhooks/creating-webhooks)

- **Declarative Pipeline Syntax**:
  - [Declarative Pipeline Syntax](https://www.jenkins.io/doc/book/pipeline/syntax/#declarative-pipeline)

---

### Conclusion:

By following the steps outlined above, you can set up a basic CI/CD pipeline in Jenkins to automate the build, test, and deployment processes for your application. Be sure to modify the pipeline script to fit the needs of your application (e.g., using different build tools, test frameworks, and deployment strategies). The GitHub documentation will be helpful for more specific configuration options, such as integrating GitHub with Jenkins or using webhooks.
